# Análise de Código - Roteamento de Tráfego via TOR com Python/Requests para Pentest

**Data de Publicação:** 18 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi
**Ferramenta de Análise**: [`TOR`](https://www.torproject.org/download/)

---
## 1. Introdução

Em testes de invasão (pentest), a capacidade de anonimizar a origem do tráfego é fundamental para emular atacantes reais e evadir sistemas de detecção baseados em reputação de IP. O código a seguir apresenta uma função em Python que utiliza a biblioteca `requests` para rotear todo o seu tráfego HTTP/HTTPS através da rede TOR (The Onion Router), mascarando efetivamente o endereço de IP público do pentester.

```python
import requests

def get_tor_session():
    """
    Cria e retorna um objeto de sessão da biblioteca requests
    configurado para usar a rede TOR como proxy.
    """
    # Cria uma instância do objeto Session
    session = requests.Session()

    # Define o proxy para os protocolos HTTP e HTTPS.
    # O tráfego será direcionado para um proxy SOCKS5 local,
    # que é a porta de entrada padrão para o serviço TOR.
    session.proxies = {
        "http": "socks5://localhost:9050", 
        "https": "socks5://localhost:9050"
    }
                       
    return session
```

## 2. Pré-requisitos e Contexto Operacional

Para que o código funcione, é **mandatório** que o serviço TOR esteja em execução na máquina local (localhost) e escutando na porta `9050`. O script Python não inicia o TOR; ele apenas o utiliza como um proxy.

* **Opções de Instalação:**
  * **Serviço TOR (Daemon):** A abordagem recomendada para automação e scripts. Em sistemas baseados em Debian (como **Kali Linux**), pode ser instalado com sudo `apt-get install tor` e iniciado com `sudo systemctl start tor`.
  * **TOR Browser:** Abrir o TOR Browser também inicia o serviço de proxy, tornando-o acessível para o script.

## 3. Análise Detalhada do Código

1. **`session = requests.Session()`:** O uso de um objeto `Session` é uma boa prática. Ele permite a persistência de configurações (como proxies, cookies e cabeçalhos) em múltiplas requisições, otimizando a performance e a organização do código.

2. **`session.proxies = {...}`:** Este é o núcleo da funcionalidade. O atributo `.proxies` do objeto de sessão é um dicionário que mapeia protocolos de URL (`http`, `https`) para os endereços de proxy que devem ser usados.

3. **`"socks5://localhost:9050"`:** Esta string define os parâmetros do proxy:
    * **`socks5`:** Protocolo do proxy. SOCKS5 opera na camada de sessão (**Camada** 5 do **modelo OSI**), permitindo encaminhar qualquer tipo de tráfego TCP, sendo mais flexível que proxies HTTP. É o protocolo padrão utilizado pelo TOR.
    * **`localhost`:** O host onde o serviço de proxy está rodando (a própria máquina).
    * **`9050`:** A porta de comunicação padrão do proxy SOCKS do TOR.

## 4. Demonstração Prática

O script a seguir valida a eficácia da mudança de IP, comparando uma requisição direta com uma requisição feita através da sessão TOR.

```Python
# (Supondo que a função get_tor_session() já foi definida)

# Requisição com IP normal
ip_normal = requests.get("[https://api.ipify.org](https://api.ipify.org)").text
print(f"[+] IP de Origem (Direto): {ip_normal}")

# Requisição através da rede TOR
print("[*] Conectando via TOR...")
tor_session = get_tor_session()
ip_tor = tor_session.get("[https://api.ipify.org](https://api.ipify.org)").text
print(f"[+] IP de Origem (Via TOR): {ip_tor}")

if ip_normal != ip_tor:
    print("\n[SUCESSO] O IP foi alterado pela rede TOR.")
else:
    print("\n[FALHA] O IP não mudou. Verifique se o serviço TOR está ativo.")
```

## 5. Aplicações em Testes de Invasão (Pentest)
A utilização desta ferramenta é estratégica em diversas fases de um pentest:

1. **Ocultação de Origem:** Evita que o IP real do time de pentest seja registrado nos logs do alvo (servidores web, firewalls, SIEM), dificultando a correlação das atividades com a equipe de teste.
2. **Evasão de Defesas Baseadas em IP:**
    * **Web Application Firewalls (WAFs):** *WAFs* frequentemente bloqueiam IPs que exibem comportamento malicioso (ex: injeção de SQL, fuzzing). A capacidade de rotacionar o IP de saída via TOR permite contornar esses bloqueios.
    * **Rate Limiting:** Aplicações que limitam o número de requisições por IP (ex: em formulários de login para evitar brute force) podem ser testadas de forma mais eficaz.
3. **Simulação de Atores de Ameaça (Threat Emulation):** Muitos atacantes reais utilizam TOR ou redes de proxy para anonimato. Usar a mesma técnica durante um pentest fornece uma avaliação mais realista da postura de segurança da organização contra ameaças anônimas.
4. **Contorno de Restrições Geográficas:** Permite testar controles de segurança baseados em geolocalização, simulando acessos de diferentes países, dependendo da rota e do nó de saída que a rede TOR fornecer.

## 6. Conclusão

A função `get_tor_session` é uma ferramenta simples, porém poderosa, para o arsenal de um profissional de cibersegurança. Ela encapsula a complexidade de interagir com a rede TOR, permitindo que scripts de automação para pentest operem com um grau essencial de anonimato, resiliência e capacidade de evasão.

