# Guia Essencial de Comandos Linux (Ubuntu/Debian): Gerenciamento e Segurança

**Público-alvo:** Profissionais de TI, de estudantes a administradores de sistemas.
**Objetivo:** Fornecer uma referência prática e didática para as operações mais comuns no terminal, com ênfase em boas práticas e segurança.

## Introdução

O terminal Linux é a ferramenta mais poderosa à disposição de um administrador de sistemas. Dominá-lo não é apenas uma questão de eficiência, mas um pilar para a segurança e a estabilidade de qualquer ambiente. Este guia foi estruturado em seções lógicas, partindo do básico e avançando para conceitos mais complexos, sempre com um olhar atento à segurança.

---

## Seção 1: Manipulação de Arquivos e Diretórios (O Básico Essencial)

A base de qualquer sistema operacional são seus arquivos. Saber como navegar e manipulá-los é o primeiro passo.

### 1.1 Navegação
* `pwd` (Print Working Directory): Mostra o diretório exato em que você está.
* `ls` (List): Lista o conteúdo de um diretório.
    * **Opções Comuns:**
        * `ls -l`: Lista em formato longo, mostrando permissões, dono, tamanho e data.
        * `ls -a`: Mostra todos os arquivos, incluindo os ocultos (que começam com `.`).
        * `ls -h`: Usado com `-l`, mostra os tamanhos em formato legível (KB, MB, GB).
    * **Exemplo Prático:** `ls -lah` (combinação das três).
* `cd` (Change Directory): Navega entre os diretórios.
    * `cd /caminho/para/o/diretorio`: Vai para o diretório especificado.
    * `cd ..`: Volta um nível no diretório.
    * `cd ~` ou apenas `cd`: Retorna para o seu diretório "home".

### 1.2 Criação e Remoção
* `touch [arquivo]`: Cria um arquivo vazio ou atualiza a data de modificação de um arquivo existente.
* `mkdir [diretorio]`: Cria um novo diretório.
    * `mkdir -p /caminho/profundo/novo`: A opção `-p` cria todos os diretórios pais no caminho, caso não existam.
* `rm [arquivo]`: Remove um arquivo.
* `rmdir [diretorio]`: Remove um diretório **vazio**.
* `rm -r [diretorio]`: Remove um diretório e todo o seu conteúdo (recursivamente).

> **⚠️ Alerta de Segurança e Senioridade:** O comando `rm -rf /` é devastador. Ele tentará apagar **todo** o sistema de arquivos a partir da raiz, sem pedir confirmação. A opção `-f` (force) ignora avisos. Use `rm -r` com extremo cuidado, especialmente com `sudo`. Sempre verifique duas vezes o diretório em que você está com `pwd` antes de um `rm -r`.

### 1.3 Cópia e Movimentação
* `cp [origem] [destino]`: Copia arquivos ou diretórios.
    * `cp /caminho/arquivo.txt /novo/caminho/`: Copia um arquivo.
    * `cp -r /caminho/diretorio /novo/caminho/`: Copia um diretório e seu conteúdo.
* `mv [origem] [destino]`: Move ou renomeia um arquivo/diretório.
    * `mv arquivo.txt /novo/lugar/`: Move o arquivo.
    * `mv arquivo.txt arquivo_renomeado.txt`: Renomeia o arquivo no mesmo local.

### 1.4 Visualização e Busca
* `cat [arquivo]`: Exibe o conteúdo completo de um arquivo na tela.
* `less [arquivo]`: Exibe o conteúdo de um arquivo de forma paginada. Permite navegar para cima e para baixo. É mais eficiente para arquivos grandes que o `cat`.
* `grep "[padrão]" [arquivo]`: Procura por um padrão de texto dentro de um arquivo.
    * **Exemplo:** `grep "error" /var/log/syslog` busca a palavra "error" no log do sistema.
* `find [caminho] -name "[nome_arquivo]"`: Procura por arquivos e diretórios em um caminho específico.
    * **Exemplo:** `find /home -name "*.pdf"` encontra todos os arquivos PDF na pasta `/home`.

---

## Seção 2: Gerenciamento de Permissões (O Pilar da Segurança)

No Linux, tudo é um arquivo, e todo arquivo tem um dono e permissões. Entender isso é fundamental para a segurança.

### 2.1 Entendendo as Permissões

Ao usar `ls -l`, você vê algo como `-rwxr-xr--`. Isso se divide em:
* **Primeiro caractere:** `d` para diretório, `-` para arquivo.
* **Três blocos seguintes:** Permissões para o **Dono** (user), **Grupo** (group) e **Outros** (others).
* **Permissões:** `r` (read/leitura), `w` (write/escrita), `x` (execute/execução).

### 2.2 Comandos Essenciais
* `chmod` (Change Mode): Altera as permissões de um arquivo/diretório.
    * **Modo Simbólico (mais intuitivo):**
        * `chmod u+x arquivo`: Adiciona (`+`) permissão de execução (`x`) para o dono (`u`).
        * `chmod g-w arquivo`: Remove (`-`) permissão de escrita (`w`) para o grupo (`g`).
        * `chmod o=r arquivo`: Define (`=`) a permissão para outros (`o`) como apenas leitura (`r`).
    * **Modo Octal (mais rápido para seniores):** Cada permissão tem um valor: `r=4`, `w=2`, `x=1`. Some-os.
        * `rwx` = 4+2+1 = `7`
        * `r-x` = 4+0+1 = `5`
        * `r--` = 4+0+0 = `4`
        * **Exemplo:** `chmod 755 script.sh` resulta em `rwxr-xr-x` (dono pode tudo, grupo e outros podem ler e executar).
* `chown` (Change Owner): Altera o dono e o grupo de um arquivo/diretório.
    * **Exemplo:** `chown novo_dono:novo_grupo arquivo.txt`.
    * **Para diretórios (recursivo):** `chown -R usuario:grupo /caminho/do/diretorio`.

> **💡 Dica de Senioridade:** A gestão de permissões segue o **Princípio do Menor Privilégio**. Nunca conceda permissões `777` (`rwxrwxrwx`) a arquivos ou diretórios em um servidor de produção. Isso permite que qualquer usuário no sistema leia, modifique e execute o arquivo, criando uma falha de segurança grave.

---

## Seção 3: Gerenciamento de Sistema e Usuários

### 3.1 Sistema e Processos
* `df -h`: Mostra o uso de espaço em disco das partições montadas.
* `du -sh [diretorio]`: Mostra o espaço total usado por um diretório específico.
* `top` ou `htop`: Exibe um painel em tempo real dos processos, uso de CPU e memória. (`htop` é mais visual e interativo; instale com `sudo apt install htop`).
* `ps aux`: Lista todos os processos em execução no sistema.
* `kill [PID]`: Envia um sinal para terminar um processo. Use `ps aux | grep nome_do_processo` para achar o PID (Process ID).
* `systemctl [acao] [servico]`: O controlador padrão para serviços (daemons) em sistemas modernos.
    * **Ações:** `start`, `stop`, `restart`, `status`, `enable` (iniciar no boot), `disable`.
    * **Exemplo:** `sudo systemctl status apache2` verifica o status do servidor web Apache.

### 3.2 Usuários e Grupos
* `sudo [comando]`: Executa um comando com privilégios de superusuário (root). É a forma **correta** de realizar tarefas administrativas, em vez de logar diretamente como root.
* `adduser [nome_usuario]`: Script interativo para adicionar um novo usuário. Ele cria o diretório home, define a senha e é a forma recomendada para Debian/Ubuntu.
* `deluser [nome_usuario]`: Remove um usuário do sistema.
* `passwd [nome_usuario]`: Altera a senha de um usuário.
* `su [nome_usuario]`: Troca para a conta de outro usuário. `su -` faz um login completo, carregando o ambiente do usuário.

> **🔐 Aspecto Crítico de Segurança:** Os dados dos usuários ficam em `/etc/passwd` (lista de usuários) e as senhas criptografadas em `/etc/shadow`. O arquivo `/etc/shadow` só pode ser lido pelo root. **Nunca** edite esses arquivos manualmente a menos que saiba exatamente o que está fazendo. Use sempre os comandos (`adduser`, `usermod`, etc.) para gerenciamento.

---

## Seção 4: Aspectos Críticos de Segurança na Prática

Além dos pontos já mencionados, um administrador deve ter estes comandos e conceitos em mente:

1.  **Mantenha o Sistema Atualizado (O Mais Importante!)**
    A maioria das invasões explora vulnerabilidades já conhecidas e corrigidas.
    ```bash
    sudo apt update       # Atualiza a lista de pacotes disponíveis
    sudo apt upgrade      # Instala as atualizações de segurança e de pacotes
    ```

2.  **Verifique Portas Abertas**
    Portas abertas são potenciais pontos de entrada. Saiba o que está rodando em sua máquina.
    ```bash
    sudo ss -tulpn
    ```
    Este comando mostra todos os serviços que estão "escutando" por conexões de rede. Se vir algo que não reconhece, investigue.

3.  **Firewall Simples e Eficaz**
    O Ubuntu vem com o `ufw` (Uncomplicated Firewall), uma interface amigável para o `iptables`.
    ```bash
    sudo ufw status                # Verifica o estado do firewall
    sudo ufw enable                # Ativa o firewall
    sudo ufw allow ssh             # Permite conexões SSH (essencial antes de ativar!)
    sudo ufw allow 80/tcp          # Permite tráfego web HTTP
    sudo ufw allow 443/tcp         # Permite tráfego web HTTPS
    sudo ufw deny 3306             # Bloqueia acesso à porta do MySQL
    ```

4.  **Auditoria Básica de Logs**
    Os logs registram tudo que acontece no sistema, incluindo tentativas de invasão.
    ```bash
    # Verifica falhas de login via SSH
    grep "Failed password" /var/log/auth.log
    
    # Usa o journalctl para ver logs de um serviço específico
    journalctl -u ssh -f
    ```

## Conclusão

Este guia cobre os comandos fundamentais para a administração de um sistema Linux baseado em Debian/Ubuntu. Para o profissional iniciante, ele serve como um roteiro de aprendizado. Para o sênior, como um lembrete das boas práticas de segurança que devem permear cada ação no terminal.

A verdadeira senioridade não está em memorizar centenas de comandos, mas em compreender o **porquê** de cada um, suas implicações e, acima de tudo, em operar o sistema de forma segura, deliberada e eficiente. O terminal é seu principal aliado; trate-o com respeito e ele lhe dará controle total sobre seu ambiente.