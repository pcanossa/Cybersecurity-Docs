# Ataques ao Protocolo ARP

**Data de Publicação:** 11 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução

O Protocolo de Resolução de Endereços (ARP) é um dos pilares silenciosos e essenciais da comunicação em redes locais (LANs). Sua função é crítica e direta: traduzir um endereço de Camada 3 (o endereço IP, que é lógico e roteável) para um endereço de Camada 2 (o endereço MAC, que é físico e local). Sem o ARP, os dispositivos em uma mesma rede não saberiam como se "encontrar" fisicamente. O problema fundamental do ARP reside em seu design, criado em uma era de confiança: ele não possui nenhum mecanismo de autenticação. O protocolo confia cegamente em qualquer informação que recebe, tornando-o um alvo primário para atacantes que buscam interceptar o tráfego dentro de uma rede local.

---

### 1. O Funcionamento Legítimo do ARP: A Ponte entre IP e MAC

Para entender o ataque, é preciso primeiro entender o funcionamento normal. Quando um Host A quer enviar um pacote para o Host B na mesma rede:

1.  **Consulta ao Cache ARP:** O Host A primeiro verifica sua tabela ARP local (um cache) para ver se já conhece o endereço MAC correspondente ao IP do Host B.
2.  **Requisição ARP (ARP Request):** Se o mapeamento não está no cache, o Host A envia um pacote de **ARP Request** em broadcast para toda a rede. Essa mensagem basicamente pergunta: "Quem na rede tem o endereço IP `192.168.1.10`? Por favor, me informe seu endereço MAC."
3.  **Resposta ARP (ARP Reply):** Todos os dispositivos na rede recebem a requisição, mas apenas o Host B, que possui o IP `192.168.1.10`, responderá. Ele envia uma mensagem **ARP Reply** diretamente (unicast) para o Host A, dizendo: "Eu tenho o IP `192.168.1.10`, e meu endereço MAC é `BB:BB:BB:BB:BB:BB`."
4.  **Atualização do Cache:** O Host A recebe a resposta, armazena o mapeamento (`192.168.1.10 -> BB:BB:BB:BB:BB:BB`) em seu cache ARP para uso futuro, e a comunicação pode começar.

---

### 2. O Mecanismo do Ataque: Envenenamento do Cache ARP (ARP Cache Poisoning)

A vulnerabilidade central do ARP é que as respostas (ARP Replies) não são validadas. Qualquer dispositivo pode enviar uma resposta ARP a qualquer momento, mesmo sem ter recebido uma requisição, e os hosts que a receberem irão, confiantemente, atualizar seus caches. Este processo é chamado de **ARP Spoofing** ou **ARP Cache Poisoning**.

O ataque clássico para se tornar um **Man-in-the-Middle (MitM)** funciona das seguintes formas:

1.  **O Alvo:** O atacante (IP `.100`, MAC `CC:...`) quer interceptar o tráfego entre uma Vítima (IP `.50`, MAC `AA:...`) e o Roteador/Gateway (IP `.1`, MAC `BB:...`).
2.  **Envenenando a Vítima:** O atacante envia uma série de pacotes ARP Reply falsificados para a Vítima. A mensagem diz: "Olá, Vítima! O endereço IP do Roteador (`.1`) agora pertence ao meu endereço MAC (`CC:...`)". A Vítima, confiantemente, atualiza seu cache: `192.168.1.1 -> CC:CC:CC:CC:CC:CC`.
3.  **Envenenando o Roteador:** Simultaneamente, o atacante envia pacotes ARP Reply falsificados para o Roteador. A mensagem diz: "Olá, Roteador! O endereço IP da Vítima (`.50`) agora pertence ao meu endereço MAC (`CC:...`)". O Roteador atualiza seu cache: `192.168.1.50 -> CC:CC:CC:CC:CC:CC`.
4.  **Envenando a Tabela CAM do Switch:** O atacante altera o endereço MAC de sua própria placa de rede para ser idêntico ao de uma vítima (por exemplo, o endereço MAC do roteador `BB:...`) e envia um quadro qualquer pela rede a partir de sua máquina. O switch recebe este quadro, e vê o MAC de origem (`BB:...`) chegando pela porta do atacante. O switch, assumindo que o dispositivo se moveu fisicamente, diligentemente **atualiza sua tabela CAM**, associando o MAC da vítima à porta do atacante, dessa forma, direcionando todo tráfego endereção ao roteador identificado pelo MAC Address `BB:...`, ao dispositivo do atacante.
5.  **Sobrecarregando a Tabela CAM do Switch:** Uma variação deste ataque é o **MAC Flooding**. Em vez de usar um MAC específico, o atacante inunda o switch com milhares de quadros, cada um com um endereço MAC de origem falso e aleatório. O objetivo é encher completamente a tabela CAM do switch. Quando a tabela está cheia, o switch não sabe mais para onde enviar os pacotes e entra em um modo de *"fail-open"*, agindo como um **hub burro**: ele passa a encaminhar todos os pacotes para todas as portas. Isso permite que o atacante, com um sniffer de rede, capture todo o tráfego do segmento de rede.


**Resultado:** A Vítima agora pensa que o atacante é o Roteador, e o Roteador pensa que o atacante é a Vítima. Todo o tráfego entre eles passa primeiro pela máquina do atacante, que pode então inspecionar, modificar ou descartar os pacotes antes de repassá-los ao seu destino real.

---

### 3. Tipos de Ataques Habilitados pelo ARP Poisoning

Uma vez que o atacante se estabelece como Man-in-the-Middle, ele pode lançar diversos ataques:

* **Espionagem de Tráfego (Sniffing):** O atacante pode capturar todo o tráfego da vítima. Se as conexões não forem criptografadas (HTTP, FTP, Telnet), senhas, cookies de sessão e dados sensíveis podem ser roubados em texto plano.
* **Manipulação de Dados:** O atacante pode alterar os pacotes em trânsito. Isso pode ser usado para injetar malware em downloads, modificar informações em sites ou redirecionar a vítima para páginas de phishing. Uma técnica comum é o **SSL Stripping**, onde o atacante força o navegador da vítima a usar uma conexão HTTP insegura em vez de HTTPS.
* **Negação de Serviço (DoS):** O atacante pode simplesmente descartar todos os pacotes da vítima, cortando seu acesso à rede. Alternativamente, ele pode envenenar o cache ARP da rede mapeando o IP do gateway para um endereço MAC inexistente.
* **Sequestro de Sessão (Session Hijacking):** Ao capturar o cookie de sessão de uma vítima, o atacante pode se passar por ela em serviços web já autenticados.

---

### 4. Estratégias de Mitigação: Protegendo a Camada 2

Felizmente, embora o protocolo ARP seja inerentemente inseguro, os switches de rede modernos incluem funcionalidades avançadas para combater esses ataques.

* **Inspeção Dinâmica de ARP (Dynamic ARP Inspection - DAI):** Esta é a defesa mais eficaz e escalável.
    * **Como funciona:** O DAI é uma funcionalidade de segurança que valida os pacotes ARP na rede. Ele funciona em conjunto com o **DHCP Snooping**, que cria uma tabela confiável de mapeamentos entre endereços IP, MAC e portas do switch.
    * **Validação:** Quando um pacote ARP chega a uma porta do switch com DAI ativado, a informação (IP de origem, MAC de origem) é comparada com a tabela de confiança do DHCP Snooping.
    * **Bloqueio:** Se um pacote ARP contiver uma combinação inválida, ele é considerado malicioso e o switch o descarta, impedindo o envenenamento.

* **Tabelas ARP Estáticas:**
    * **Como funciona:** Para servidores críticos ou para o gateway, um administrador pode configurar manualmente uma entrada ARP estática e permanente na tabela ARP dos dispositivos.
    * **Vantagem:** É uma defesa à prova de falhas para mapeamentos específicos, pois uma entrada estática não pode ser sobrescrita por uma resposta ARP dinâmica.
    * **Desvantagem:** Não é uma solução escalável para redes grandes com muitos hosts, pois exige configuração manual em cada máquina.

* **Ferramentas de Detecção de Intrusão (IDS/IPS):** Sistemas de detecção de intrusão podem ser configurados para detectar os sinais de um ataque de ARP Poisoning, como um grande volume de respostas ARP não solicitadas, e alertar os administradores.

### Conclusão

O ARP Poisoning permanece como um dos ataques mais eficientes e perigosos dentro de uma rede local. Ele explora a confiança fundamental sobre a qual as LANs foram construídas. A defesa contra ele demonstra um princípio central da segurança em profundidade: não se deve confiar em nenhuma camada do modelo de rede. Através da implementação de funcionalidades de segurança modernas em switches, como a Inspeção Dinâmica de ARP, as organizações podem impor a validação e a autenticidade que o protocolo ARP originalmente não oferecia, protegendo assim a integridade de suas redes internas.