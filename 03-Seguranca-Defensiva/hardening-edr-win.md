# Hardening de Endpoints Windows

## Introdução

Enquanto os princípios de hardening de sistemas fornecem uma base filosófica para a segurança, a implementação eficaz no mundo real exige a aplicação de controles técnicos específicos e de alto impacto. Um endpoint "endurecido" não é apenas um sistema com antivírus; é um ambiente hostil para o adversário, projetado para prevenir a execução inicial, impedir o movimento lateral e gerar alertas claros ao primeiro sinal de atividade maliciosa.

Este artigo detalha um conjunto de práticas de hardening acionáveis, com foco em ambientes Microsoft Windows, que aumentam drasticamente o custo e a complexidade para um atacante, transformando o endpoint de um alvo fácil em uma fortaleza digital.

---

### 1. Limitar o Reconhecimento e Movimento Lateral na Rede Local

Ataques modernos raramente se limitam ao primeiro host comprometido. O objetivo do adversário é se mover lateralmente pela rede. Os controles a seguir visam quebrar essa cadeia de ataque.

* **Desabilitar LLMNR e NetBIOS:**
    * **O Risco:** Link-Local Multicast Name Resolution (LLMNR) e NetBIOS são protocolos legados de resolução de nomes que são extremamente vulneráveis a ataques de spoofing. Ferramentas como o `Responder.py` podem interceptar as requisições desses protocolos na rede local, enganar o host e capturar os hashes de senha dos usuários que tentam se conectar a um recurso.
    * **A Contramedida:** Desabilite esses protocolos via Política de Grupo (GPO). Forçar a rede a usar exclusivamente o DNS para resolução de nomes elimina um dos vetores de roubo de credenciais e movimento lateral mais comuns.

* **Utilizar Firewalls Baseados em Host para Segmentação:**
    * **O Risco:** Por padrão, em uma rede corporativa plana, uma estação de trabalho pode se comunicar livremente com outra. Se um worm ou um atacante compromete uma máquina, ele pode facilmente escanear e atacar outras estações de trabalho.
    * **A Contramedida:** Configure o firewall do Windows com uma política de "negação por padrão" para o tráfego de entrada e, crucialmente, **bloqueie a comunicação de estação de trabalho para estação de trabalho**. Permita apenas a comunicação com servidores essenciais (controladores de domínio, servidores de arquivos, etc.). Isso cria uma micro-segmentação que contém uma infecção ao seu ponto de origem.

---

### 2. Gerenciamento de Privilégios e Controle de Aplicações

O controle sobre o que pode ser executado e com quais privilégios é a essência da prevenção.

* **Implementar LAPS (Local Administrator Password Solution):**
    * **O Risco:** Em muitas redes, a senha da conta de administrador local é a mesma para todas as estações de trabalho. Se um atacante compromete essa senha em uma única máquina, ele instantaneamente ganha privilégios de administrador em **todas** as outras, permitindo o movimento lateral em massa.
    * **A Contramedida:** LAPS é uma ferramenta gratuita da Microsoft que resolve este problema de forma elegante. Ela randomiza a senha da conta de administrador local em cada computador, armazena essa senha de forma segura no Active Directory e a rotaciona periodicamente. Isso torna a senha única para cada máquina, quebrando o vetor de ataque. Juntamente com a **remoção de privilégios de administrador de usuários regulares**, esta é uma das defesas de maior impacto.

* **Implementar Application Whitelisting (de forma pragmática):**
    * **O Risco:** A maioria dos malwares e exploits precisa executar um código no sistema.
    * **A Contramedida:** Uma lista branca (whitelisting), que permite apenas a execução de aplicações conhecidas e autorizadas, é a defesa mais poderosa. Embora uma implementação completa possa ser complexa, uma abordagem pragmática oferece enormes benefícios: **bloqueie a execução de programas a partir de diretórios onde os usuários podem escrever**, como `Downloads`, `Desktop` e, especialmente, as pastas `AppData`. É nesses locais que os payloads maliciosos são inicialmente salvos. Bloqueie também a execução de tipos de script perigosos (`.hta`, `.vbs`, `.js`, etc.) usando ferramentas como o AppLocker ou Software Restriction Policies (SRP).

* **Atenção aos LOLBins (Living Off the Land Binaries):**
    * **O Risco:** Ao implementar o whitelisting, os atacantes se adaptaram. Eles abusam de ferramentas legítimas do próprio Windows (LOLBins) que já estão na lista branca para executar ações maliciosas. Por exemplo, `certutil.exe` pode ser usado para baixar um malware, ou `wmic.exe` para executar scripts.
    * **A Contramedida:** O whitelisting deve ser inteligente. Além de permitir a execução de um LOLBin, é preciso monitorar e restringir *como* ele é usado. Por exemplo, o firewall do host pode ser configurado para **bloquear o acesso de saída à internet** para ferramentas como `certutil.exe` e `bitsadmin.exe`.

---

### 3. Fortalecendo as Defesas Nativas e a Detecção

A plataforma Windows moderna inclui defesas poderosas que devem ser ativadas e complementadas.

* **Configurar PowerShell em "Constrained Language Mode":**
    * **O Risco:** O PowerShell é uma ferramenta de automação extremamente poderosa, o que o torna o favorito dos atacantes para ataques "fileless" (sem arquivo).
    * **A Contramedida:** Usando o AppLocker ou o Windows Defender Application Control (WDAC), é possível forçar o PowerShell a rodar em "Modo de Linguagem Restrita". Este modo limita severamente os comandos que podem ser executados, impedindo o acesso a APIs do Windows e outras funcionalidades perigosas frequentemente abusadas por malware.

* **Habilitar Regras de Redução da Superfície de Ataque (ASR):**
    * **O Risco:** Ataques frequentemente abusam de funcionalidades de softwares comuns, como o Microsoft Office, para iniciar uma infecção.
    * **A Contramedida:** Se você usa o Microsoft Defender, as regras de ASR são um conjunto de controles de alto valor. Habilite regras como: "Bloquear processos filhos de aplicações do Office", "Bloquear a execução de scripts ofuscados" e "Bloquear chamadas de API Win32 de macros do Office".

* **Implantar um EDR com Integração AMSI:**
    * **O Risco:** Scripts maliciosos são quase sempre ofuscados para evitar a detecção por assinaturas.
    * **A Contramedida:** A **AMSI (Antimalware Scan Interface)** é uma tecnologia da Microsoft que mudou o jogo da detecção. Ela funciona como um "gancho" que permite que um produto de segurança inspecione o conteúdo de um script (PowerShell, VBScript, etc.) **na memória**, no último momento possível antes da execução, **depois** que ele já foi desofuscado. Um **EDR (Endpoint Detection and Response)** que se integra com a AMSI tem uma visibilidade sem precedentes para detectar e bloquear malwares "fileless" e ofuscados. É altamente recomendável escolher apenas produtos que suportem essa integração.

### Conclusão

O hardening de endpoints é um processo contínuo de tornar o ambiente o mais restritivo e "barulhento" possível para um atacante. Ao implementar controles técnicos específicos como LAPS, AppLocker, regras de ASR e um EDR com visibilidade AMSI, uma organização eleva drasticamente o padrão de sua defesa. Cada uma dessas medidas, por si só, fecha uma porta importante para os adversários; juntas, elas criam uma defesa em profundidade resiliente, que não apenas previne a infecção inicial, mas também detecta e contém as ameaças que conseguem passar pela primeira barreira.