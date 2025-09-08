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
| **LDAP com SSL/TLS