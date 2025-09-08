# Artigo Técnico: O Modelo OSI - Estrutura, Camadas e Protocolos de Rede

## Introdução

O Modelo de Referência OSI (Open Systems Interconnection) é um framework conceitual criado para padronizar as funções de um sistema de telecomunicações ou de computação em sete camadas de abstração. Embora o modelo TCP/IP seja o padrão prático da internet moderna, o Modelo OSI permanece como uma ferramenta pedagógica e de referência indispensável para profissionais de rede e segurança. Ele fornece uma linguagem comum para descrever os processos complexos da comunicação de rede, permitindo a análise detalhada de como os dados são encapsulados, transmitidos e processados, desde o cabo físico até a aplicação final.

Este artigo detalha cada uma das sete camadas, apresentando os protocolos que operam em cada uma, com base nas informações do documento fornecido.

---

### Tabela de Protocolos por Camada OSI

A tabela a seguir consolida e organiza os protocolos de acordo com sua camada correspondente no modelo OSI.

| Camada OSI | Sigla | Nome | Explicação Breve |
| :--- | :--- | :--- | :--- |
| **7- Aplicação** | DNA | Digital Network Architecture | [cite_start]Arquitetura de rede da Digital Equipment. [cite: 1] |
| | SCP | Session Control Protocol | [cite_start]Gerencia sessões no DECnet. [cite: 1] |
| | HTTP | Hyper Text Transfer Protocol | [cite_start]Transfere páginas web. [cite: 1] |
| | SMTP | Simple Mail Transfer Protocol | [cite_start]Envia e-mails. [cite: 1] |
| | DNS | Domain Name System | [cite_start]Traduz nomes de domínio em IPs. [cite: 1] |
| | FTP | File Transfer Protocol | [cite_start]Transfere arquivos. [cite: 1] |
| | SNMP | Simple Network Management Protocol | [cite_start]Faz gerência de redes. [cite: 1] |
| | DHCP | Dynamic Host Configuration Protocol | [cite_start]Atribui IPs dinamicamente. [cite: 1] |
| | TFTP | Trivial File Transfer Protocol | [cite_start]Transfere arquivos de forma simples. [cite: 1] |
| | NFS | Network File System | [cite_start]Compartilha arquivos em rede. [cite: 1] |
| | AFP | Apple Filing Protocol | [cite_start]Compartilha arquivos em AppleTalk. [cite: 1] |
| | DNS (Novell)| Domain Name System | [cite_start]Mesma função de resolução de nomes. [cite: 1] |
| **6- Apresentação**| | | [cite_start]Não há protocolos específicos listados. [cite: 1] |
| **5- Sessão** | SCP | (já listado) | [cite_start]Associado ao gerenciamento de sessões. [cite: 1] |
| **4- Transporte** | NSP | Network Services Protocol | [cite_start]Transporte confiável no DECnet. [cite: 1] |
| | TCP | Transmission Control Protocol | [cite_start]Transporte confiável, orientado a conexão. [cite: 1] |
| | UDP | User Datagram Protocol | [cite_start]Transporte não confiável e sem conexão. [cite: 1] |
| | ATP | AppleTalk Transaction Protocol | [cite_start]Troca confiável de mensagens. [cite: 1] |
| | AEP | AppleTalk Echo Protocol | [cite_start]Testa conectividade (similar ao ping). [cite: 1] |
| | NBP | Name Binding Protocol | [cite_start]Mapeia nomes em endereços AppleTalk. [cite: 1] |
| | RTMP | Routing Table Maintenance Protocol| [cite_start]Mantém tabelas de roteamento AppleTalk. [cite: 1] |
| **3- Rede** | SPX | Sequenced Packet Exchange | [cite_start]Transporte confiável em NetWare. [cite: 1] |
| | DRP | Data Routing Protocol | [cite_start]Roteamento no DECnet. [cite: 1] |
| | DDCMP | Digital Data Communications Message Protocol | [cite_start]Enlace confiável da DEC. [cite: 1] |
| | IPv4/IPv6 | Internet Protocol v4/v6 | [cite_start]Endereçamento e roteamento IP. [cite: 1] |
| | ICMPv4/v6 | Internet Control Message Protocol | [cite_start]Mensagens de controle/erro na rede. [cite: 2] |
| | AARP | AppleTalk Address Resolution Protocol | [cite_start]Traduz endereços AppleTalk em físicos. [cite: 2] |
| | IPX | Internetwork Packet Exchange | [cite_start]Protocolo de rede Novell. [cite: 2] |
| **2- Enlace** | LLC | Logical Link Control | [cite_start]Controle lógico do enlace de dados. [cite: 2] |
| | MAC | Media Access Control | [cite_start]Acesso físico ao meio de transmissão. [cite: 2] |
| | IEEE 802.3 | Ethernet | [cite_start]Rede cabeada padrão. [cite: 2] |
| | IEEE 802.11| Wi-Fi | [cite_start]Rede sem fio. [cite: 2] |
| | IEEE 802.15| WPAN (Bluetooth) | [cite_start]Redes pessoais sem fio. [cite: 2] |
| **1- Física** | | | [cite_start]Implementação física do meio de transmissão. [cite: 2] |

---

### Análise das Camadas e a Relevância para a Cibersegurança

Compreender em qual camada um protocolo opera é crucial para a segurança, pois os ataques e as defesas são, muitas vezes, específicos para cada camada.

* **Camada de Aplicação (7):** É a mais próxima do usuário e, portanto, uma das mais visadas. Ataques como Phishing (via SMTP), Injeção de SQL (via HTTP/HTTPS) e exploração de vulnerabilidades em softwares (via FTP, RDP) ocorrem aqui. A defesa nesta camada envolve o endurecimento de aplicações e a educação do usuário.
* **Camadas de Apresentação (6) e Sessão (5):** Embora muitas vezes abstraídas no modelo TCP/IP, suas funções são vitais. A Camada de Apresentação lida com a formatação e criptografia (TLS/SSL) dos dados, enquanto a Camada de Sessão gerencia o diálogo entre os computadores. Ataques de sequestro de sessão (Session Hijacking) visam os mecanismos desta camada.
* **Camada de Transporte (4):** O campo de batalha do TCP e do UDP. Ataques de Negação de Serviço (DoS/DDoS) frequentemente exploram as características desses protocolos, como o TCP SYN Flood, que visa o processo de handshake, ou o UDP Flood, que simplesmente satura a banda.
* **Camada de Rede (3):** Onde o endereçamento (IP) e o roteamento acontecem. Ataques como IP Spoofing, Ping Sweeps (usando ICMP) e a manipulação de rotas ocorrem nesta camada. Firewalls e Listas de Controle de Acesso (ACLs) são as principais defesas aqui.
* **Camada de Enlace (2):** Focada na rede local (LAN). É o domínio dos endereços MAC. Ataques como ARP Poisoning e MAC Spoofing exploram a confiança inerente nesta camada para realizar ataques Man-in-the-Middle. Funcionalidades de segurança de switch, como DHCP Snooping e Port Security, são as defesas.
* **Camada Física (1):** Representa o meio físico da transmissão (cabos, fibra óptica, ondas de rádio). A segurança nesta camada é física: proteger contra o acesso não autorizado a cabos de rede (para "grampear" o tráfego) e a equipamentos como switches e roteadores.

### Conclusão

O Modelo OSI fornece um mapa conceitual indispensável para a rede. Para o profissional de cibersegurança, ele não é apenas uma teoria, mas uma ferramenta de diagnóstico e estratégia. Saber que um ataque de phishing começa na Camada 7, um DDoS volumétrico atinge a Camada 4, e um ARP Poisoning ocorre na Camada 2, permite a aplicação da ferramenta de defesa correta, na camada correta, para construir uma postura de segurança verdadeiramente robusta e em profundidade.