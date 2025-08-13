# Mitigação de Ataques de Negação de Serviço (DoS/DDoS)

**Data de Publicação:** 13 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução

Um ataque de Negação de Serviço visa tornar um computador, um serviço ou uma rede inteira indisponível para seus usuários legítimos. Ele alcança isso ao sobrecarregar o alvo com tráfego espúrio ou ao enviar requisições malformadas que causam falhas ou consomem todos os seus recursos. É fundamental distinguir entre dois tipos de ataque:

* **DoS (Denial of Service):** O ataque é originado de uma **única fonte**.
* **DDoS (Distributed Denial of Service):** O ataque é orquestrado a partir de **centenas ou milhares de fontes distribuídas** (geralmente uma botnet).

Essa distinção é o fator mais importante para definir a estratégia de mitigação, pois as defesas que funcionam para um DoS são, em grande parte, ineficazes contra um DDoS em larga escala.

---

### 1. Tipos de Ataques de Negação de Serviço

Os ataques DoS/DDoS podem ser classificados pelo recurso que eles visam exaurir.

* **Ataques Volumétricos:** O tipo mais comum de *DDoS*. O objetivo é simplesmente saturar a largura de banda do link de internet da vítima com um volume massivo de tráfego lixo. Exemplos incluem **inundações UDP (UDP Floods)** e **inundações ICMP (ICMP Floods)**.
* **Ataques de Protocolo:** Consomem os recursos dos próprios servidores ou dos equipamentos de rede (como firewalls e roteadores), explorando fraquezas nos protocolos. O exemplo clássico é o **TCP SYN Flood**.
* **Ataques à Camada de Aplicação:** Ataques mais sutis que visam uma aplicação específica (geralmente um servidor web). Por exemplo, uma inundação de requisições HTTP para uma página de busca que consome muitos recursos do banco de dados. Estes ataques exigem menos largura de banda para serem eficazes.

---

### 2. Mitigando Ataques de Origem Interna e DoS Simples (Defesa Local)

Esta camada de defesa foca em fortalecer a própria rede para impedir que ela seja usada como plataforma de ataque e para bloquear ataques de fonte única. 

* **Prevenção de Spoofing (a Base):** O *spoofing de IP* é um componente histórico de ataques *DoS*. As seguintes funcionalidades de switch (Camada 2) são cruciais para impedir que dispositivos na sua própria rede lancem ataques com IPs falsificados:
    * **DHCP Snooping:** Bloqueia servidores DHCP falsos.
    * **IP Source Guard:** Garante que um host só possa usar o endereço IP que lhe foi legitimamente atribuído pelo DHCP.
    * **Dynamic ARP Inspection (DAI):** Impede o envenenamento de cache ARP.

* **Listas de Controle de Acesso (ACLs):** Em um roteador ou firewall, as **ACLs** podem ser usadas para bloquear o tráfego vindo de um endereço IP específico que esteja realizando um ataque de *DoS*. Elas são eficazes para bloquear um único atacante, mas inúteis contra um *DDoS* com milhares de fontes.

* **Limitação de Taxa (Rate-Limiting):** Roteadores e firewalls podem ser configurados para limitar o número de pacotes por segundo para um determinado protocolo (ex: *ICMP*) ou de uma determinada fonte. Isso pode ajudar a absorver o impacto de ataques menores sem sobrecarregar o equipamento.

---

### 3. O Desafio Moderno: Mitigando Ataques DDoS em Larga Escala

As defesas locais falham contra um *DDoS volumétrico* por uma razão simples: o ataque satura o link de internet **antes** que o tráfego chegue ao firewall para ser filtrado. Se o link da rede é de 1 Gbps e recebe um ataque de 10 Gbps, o firewall nunca terá a chance de analisar os pacotes. O *"cano"* já está entupido.

A solução padrão da indústria é a **Mitigação em Nuvem (Cloud-based Scrubbing)**.

* **Como Funciona:**
    1.  **Detecção:** A organização, usando ferramentas de monitoramento de fluxo de rede (como *NetFlow*), detecta uma anomalia de tráfego que indica um ataque *DDoS*.
    2.  **Redirecionamento:** O tráfego de internet destinado à organização é redirecionado para a rede do provedor de mitigação de *DDoS*. Isso é feito geralmente através de uma alteração no roteamento da internet (BGP) ou no DNS.
    3.  **Limpeza (Scrubbing):** O provedor de mitigação possui uma rede global com uma capacidade massiva (**terabits** por segundo) para absorver o ataque. O tráfego passa por *"centros de limpeza"* que usam filtros sofisticados para separar os pacotes maliciosos do tráfego legítimo.
    4.  **Encaminhamento:** Apenas o tráfego limpo e legítimo é então encaminhado para a organização através de um túnel seguro ou link privado.

---

### 4. Detecção e Resposta

A detecção precoce é fundamental.

* **Monitoramento de Anomalias:** A política de segurança deve exigir o monitoramento constante do comportamento da rede para estabelecer uma linha de base (*baseline*) do que é "normal". Ferramentas de análise de utilização de rede podem, então, gerar alertas automaticamente quando o tráfego desvia significativamente dessa linha de base, indicando um possível ataque.
* **O Papel do Analista:** Durante um ataque, a função do analista é identificar rapidamente o tipo de ataque (ex: é um flood UDP? um ataque de amplificação DNS?) para aplicar a mitigação correta e, crucialmente, acionar o plano de resposta, que pode incluir a comunicação com o provedor de mitigação em nuvem para iniciar o redirecionamento do tráfego.

### Conclusão

A estratégia de mitigação de *Negação de Serviço* (*DoS* ou *DDoS*) depende inteiramente da escala e da natureza do ataque. Controles de segurança locais, como as tecnologias **anti-spoofing** e as **ACLs**, são essenciais para a higiene da rede e para a defesa contra ataques simples de fonte única. No entanto, para enfrentar a realidade dos ataques DDoS distribuídos em larga escala, a única defesa viável é a parceria com um **serviço de mitigação em nuvem** especializado, que possua a capacidade e a inteligência necessárias para absorver a inundação e garantir a continuidade do negócio.