# Principais Serviços, Protocolos e Portas

**Data de Publicação:** 05 de Setembro de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução

A comunicação em redes TCP/IP é definida por uma trinca de informações: o endereço IP (o destino), o protocolo da Camada de Transporte (TCP para confiabilidade, UDP para velocidade) e o número da porta (o serviço específico naquele destino). As portas, numeradas de `0` a `65535`, funcionam como "portões" lógicos, garantindo que uma requisição para um site chegue ao software do servidor web, e não ao servidor de e-mail.

---

### Tabela de Referência Expandida: Principais Serviços de Rede

#### Serviços Web e de Transferência de Arquivos

| Serviço | Acrônimo | Protocolo | Porta Padrão | Descrição Breve |
| :--- | :--- | :--- | :--- | :--- |
| **Transf. de Arquivos** | FTP | TCP | 20 (dados), 21 (controle) | Protocolo para transferência de arquivos. **(Não seguro)**. |
| **Secure Shell** | SSH | TCP | 22 | Acesso remoto seguro a terminais e transferência de arquivos (SFTP). |
| **Transferência de Hipertexto** | HTTP | TCP | 80 | Protocolo base da World Wide Web. **(Não seguro)**. |
| **Transferência de Hipertexto Segura**| HTTPS | TCP | 443 | Versão segura do HTTP, usa criptografia TLS. Essencial hoje. |
| **Transf. de Arquivos Trivial**| TFTP | UDP | 69 | Versão simplificada do FTP, sem autenticação. |
| **Server Message Block** | SMB | TCP | 445 | Compartilhamento de arquivos e impressoras (redes Windows). |
| **Network File System** | NFS | TCP/UDP | 2049 | Compartilhamento de arquivos em redes (sistemas UNIX/Linux).|

#### Serviços de E-mail

| Serviço | Acrônimo | Protocolo | Porta Padrão | Descrição Breve |
| :--- | :--- | :--- | :--- | :--- |
| **Transf. de E-mail**| SMTP | TCP | 25 | Usado para enviar e-mails entre servidores. |
| **Post Office Protocol v3** | POP3 | TCP | 110 | Usado para baixar e-mails de um servidor. **(Não seguro)**. |
| **Acesso a Mensagens da Int.** | IMAP | TCP | 143 | Usado para acessar e-mails em um servidor. **(Não seguro)**. |
| **SMTP com TLS (Submissão)**| SMTPS | TCP | 587 (às vezes 465)| Porta segura para clientes enviarem e-mail. |
| **IMAP com SSL/TLS** | IMAPS | TCP | 993 | Versão segura do IMAP. |
| **POP3 com SSL/TLS** | POP3S | TCP | 995 | Versão segura do POP3. |

#### Serviços de Acesso Remoto e Gerenciamento

| Serviço | Acrônimo | Protocolo | Porta Padrão | Descrição Breve |
| :--- | :--- | :--- | :--- | :--- |
| **Telnet** | Telnet | TCP | 23 | Acesso remoto a terminais. **(Altamente inseguro)**. |
| **Gerenciamento de Rede**| SNMP | UDP | 161 (trap), 162 (get/set)| Monitoramento e gerenciamento de dispositivos de rede. |
| **Remote Desktop Protocol** | RDP | TCP | 3389 | Protocolo da Microsoft para acesso a áreas de trabalho remotas.|
| **Virtual Network Computing**| VNC | TCP | 5900 | Outro protocolo para acesso a áreas de trabalho remotas. |

#### Serviços de Nomes, Diretório e Autenticação

| Serviço | Acrônimo | Protocolo | Porta Padrão | Descrição Breve |
| :--- | :--- | :--- | :--- | :--- |
| **Sistema de Nomes de Domínio**| DNS | TCP/UDP | 53 | Traduz nomes de domínio para IPs. (UDP p/ consultas, TCP p/ transf. de zona).|
| **Lightweight Directory Access Prot.**| LDAP | TCP/UDP | 389 | Protocolo para acessar e manter serviços de diretório. |
| **LDAP com SSL/TLS**| LDAPS | TCP | 636 | Versão segura do LDAP. |
| **Kerberos**| Kerberos | TCP/UDP | 88 | Protocolo de autenticação de rede (usado no Active Directory).|

#### Serviços de Rede Essenciais

| Serviço | Acrônimo | Protocolo | Porta Padrão | Descrição Breve |
| :--- | :--- | :--- | :--- | :--- |
| **Configuração Dinâmica** | DHCP | UDP | 67 (servidor), 68 (cliente)| Atribui endereços IP dinamicamente aos hosts. |
| **Tempo de Rede** | NTP | UDP | 123 | Sincroniza os relógios dos computadores. |
| **Internet Relay Chat**| IRC | TCP | 194 | Protocolo de comunicação por texto (chat). |
| **Session Initiation Protocol**| SIP | TCP/UDP | 5060, 5061 (seguro) | Protocolo para iniciar, modificar e terminar sessões de VoIP. |

#### Serviços de Banco de Dados

| Serviço | Acrônimo | Protocolo | Porta Padrão | Descrição Breve |
| :--- | :--- | :--- | :--- | :--- |
| **Microsoft SQL Server**| MS-SQL | TCP | 1433 | Sistema de gerenciamento de banco de dados da Microsoft. |
| **Oracle Database** | Oracle | TCP | 1521 | Sistema de gerenciamento de banco de dados da Oracle. |
| **MySQL**| MySQL | TCP | 3306 | Sistema de gerenciamento de banco de dados de código aberto. |
| **PostgreSQL**| PostgreSQL| TCP | 5432 | Sistema de gerenciamento de banco de dados objeto-relacional. |
| **Redis**| Redis | TCP | 6379 | Banco de dados em memória (chave-valor). |

---

### Por que isso é Importante?

1.  **Configuração de Firewalls e ACLs:** A política de segurança de uma rede é implementada através de regras que permitem ou bloqueiam o tráfego com base em IPs, protocolos e **portas**. Conhecer as portas padrão é o pré-requisito para criar regras eficazes.

2.  **Reconhecimento e Varredura de Portas:** A primeira fase de um ataque ativo geralmente envolve uma varredura de portas para descobrir quais serviços um alvo está executando. Um analista deve ser capaz de interpretar os resultados de uma varredura para entender a superfície de ataque de um sistema.

3.  **Endurecimento de Sistemas (Hardening):** A prática de segurança de fechar **todas** as portas que não são estritamente necessárias é uma das formas mais eficazes de reduzir a superfície de ataque. Se um servidor não precisa de acesso remoto, as portas 22, 23 e 3389 devem ser bloqueadas.

### Conclusão

O sistema de portas e protocolos é a linguagem fundamental do tráfego de rede. A fluência nesta linguagem permite que um profissional de cibersegurança não apenas construa defesas robustas, mas também leia e interprete o fluxo de dados para caçar ameaças, investigar incidentes e avaliar a postura de segurança de qualquer dispositivo conectado à rede.