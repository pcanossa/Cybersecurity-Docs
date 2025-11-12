# Framework Cyber Kill Chain®

## Introdução

Desenvolvido pela empresa de defesa Lockheed Martin e inspirado em modelos militares, o framework Cyber Kill Chain® oferece uma visão de alto nível das etapas que um adversário precisa percorrer para ser bem-sucedido em um ataque. O modelo é apresentado como uma "corrente" (chain) porque cada fase depende do sucesso da fase anterior. Isso introduz um conceito estratégico poderoso para os defensores: a defesa só precisa ter sucesso em **quebrar um dos elos** para frustrar toda a campanha de ataque.

A Kill Chain fornece um framework para analisar intrusões, identificar vulnerabilidades na estratégia de defesa e entender o fluxo sequencial de um ataque, desde o reconhecimento inicial até o objetivo final do adversário.

---

### 1. As 7 Fases da Cyber Kill Chain®

O modelo é composto por sete fases distintas e sequenciais. Para cada fase, existe um objetivo para o atacante e uma oportunidade de defesa correspondente.

#### **Fase 1: Reconnaissance (Reconhecimento)**
* **Objetivo do Atacante:** Coletar o máximo de informações sobre o alvo. Isso inclui a pesquisa por endereços de e-mail, nomes de funcionários, tecnologias utilizadas e vulnerabilidades potenciais através de métodos passivos (OSINT) e ativos (varredura de rede).
* **Ação do Defensor:** Detectar a varredura, minimizar a "superfície de ataque" exposta publicamente e monitorar a coleta de informações sobre a organização.

#### **Fase 2: Weaponization (Armamentização)**
* **Objetivo do Atacante:** Criar uma "arma" cibernética. Isso envolve acoplar um exploit (código que explora uma vulnerabilidade) a um payload (o malware a ser entregue, como um backdoor ou um trojan). Um exemplo clássico é a criação de um documento do Microsoft Office com uma macro maliciosa. Esta fase ocorre inteiramente no lado do atacante.
* **Ação do Defensor:** A defesa aqui é indireta, baseada na inteligência de ameaças para entender quais exploits e tipos de malware estão sendo ativamente "armados" e usados por adversários.

#### **Fase 3: Delivery (Entrega)**
* **Objetivo do Atacante:** Transmitir a arma para o alvo. É o método de entrada.
* **Ação do Defensor:** Detectar e bloquear o método de entrega.
* **Exemplos:** O vetor de entrega mais comum é o e-mail de **phishing**. Outros métodos incluem sites comprometidos (drive-by download), mídias removíveis (USB) e o envio de links maliciosos. A defesa se concentra em gateways de e-mail seguros, proxies web e políticas de bloqueio de USB.

#### **Fase 4: Exploitation (Exploração)**
* **Objetivo do Atacante:** Ativar a arma e explorar a vulnerabilidade no sistema da vítima.
* **Ação do Defensor:** Proteger e fortalecer os sistemas para que o exploit falhe.
* **Exemplos:** O usuário clica no anexo e habilita as macros; uma vulnerabilidade no navegador é acionada ao visitar uma página. A defesa principal aqui é uma **gestão de patches rigorosa** (para eliminar a vulnerabilidade) e o uso de softwares de segurança de endpoint (NGAV/EDR) que podem detectar e bloquear a atividade do exploit.

#### **Fase 5: Installation (Instalação)**
* **Objetivo do Atacante:** Instalar o malware no sistema da vítima para estabelecer uma presença persistente.
* **Ação do Defensor:** Detectar e bloquear a instalação do malware.
* **Exemplos:** O exploit baixa e instala um backdoor ou um trojan no disco. A defesa depende de software antivírus/NGAV, HIPS (Host-based Intrusion Prevention System) e controle de aplicações (whitelisting) para impedir a execução de binários não autorizados.

#### **Fase 6: Command & Control (Comando e Controle - C2)**
* **Objetivo do Atacante:** O malware instalado estabelece um canal de comunicação de saída para um servidor controlado pelo atacante. Através deste canal, o adversário pode controlar remotamente o sistema comprometido.
* **Ação do Defensor:** Detectar e bloquear este canal de comunicação.
* **Exemplos:** A defesa aqui se concentra na análise do tráfego de saída (egress traffic). Firewalls, proxies e DNS firewalls são usados para bloquear a comunicação com IPs e domínios de C2 conhecidos.

#### **Fase 7: Actions on Objectives (Ações nos Objetivos)**
* **Objetivo do Atacante:** Finalmente, o adversário usa seu acesso para atingir seu objetivo final.
* **Ação do Defensor:** Detectar as atividades internas do atacante, responder e conter o dano.
* **Exemplos:** Roubo e **exfiltração de dados**, destruição de sistemas (ransomware), ou uso da máquina comprometida como um pivô para realizar **movimento lateral** e atacar outros sistemas na rede. A defesa nesta fase depende da segmentação da rede, do monitoramento de atividades internas e de um plano de resposta a incidentes bem definido.

---

### 2. Valor Estratégico e Limitações do Modelo

* **Valor Estratégico:**
    * **Simplicidade:** É um modelo fácil de entender e comunicar, ideal para explicar o fluxo de um ataque para audiências não técnicas.
    * **Estrutura de Defesa:** Fornece um framework claro para construir uma estratégia de defesa em profundidade, mapeando controles de segurança para cada fase do ataque.

* **Limitações Modernas:**
    * **Linearidade:** A principal crítica é que o modelo é estritamente linear. Ataques modernos podem não seguir essa sequência exata, podem pular fases ou retornar a fases anteriores.
    * **Foco em Perímetro:** O modelo é fortemente centrado em ataques que vêm de fora e violam o perímetro da rede. Ele não modela bem ameaças internas ou ataques que começam com credenciais já comprometidas (ex: ataques em nuvem).

### 3. Complementando a Kill Chain® com o MITRE ATT&CK®

A melhor forma de ver os dois frameworks é como complementares. Se a **Cyber Kill Chain® é o índice de um livro**, descrevendo os capítulos principais de um ataque, o **MITRE ATT&CK® é o conteúdo detalhado de cada um desses capítulos**, listando as centenas de técnicas específicas que um adversário pode usar.

### Conclusão

A Cyber Kill Chain® é um modelo conceitual fundamental e altamente influente que oferece uma estrutura de alto nível para entender o ciclo de vida de um ciberataque tradicional. Seu princípio central — de que a defesa precisa quebrar apenas um elo da corrente para ter sucesso — continua sendo uma lição estratégica valiosa. Embora tenha limitações para descrever a complexidade de todas as ameaças modernas, ele permanece como um excelente ponto de partida para a construção de uma defesa em camadas, especialmente quando enriquecido com a granularidade de frameworks como o MITRE ATT&CK®.