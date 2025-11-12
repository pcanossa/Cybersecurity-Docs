# IDS e IPS

**Data de Publicação:** 18 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução

Enquanto um firewall atua como um porteiro, controlando o acesso com base em regras de origem, destino e porta, ele geralmente não inspeciona o conteúdo do tráfego permitido em busca de intenções maliciosas. Para preencher essa lacuna, as organizações recorrem aos **Sistemas de Detecção de Intrusão (IDS)** e **Sistemas de Prevenção de Intrusão (IPS)**. Essas tecnologias são os *"guardiões"* da rede, projetados para analisar o tráfego em um nível mais profundo e identificar atividades que violem a política de segurança ou que correspondam a padrões de ataque conhecidos. A escolha entre detectar uma ameaça (IDS) ou preveni-la ativamente (IPS) é uma das decisões de arquitetura de segurança mais fundamentais.

---

### 1. O Dilema Fundamental: Detecção (IDS) vs. Prevenção (IPS)

A diferença essencial entre IDS e IPS reside em seu modo de operação e, consequentemente, em sua capacidade de resposta.

#### **Sistema de Detecção de Intrusão (IDS)**
* **Modo de Operação:** *Out-of-band* (fora da banda). Um sensor IDS não fica no caminho direto do tráfego. Em vez disso, ele recebe uma **cópia** do tráfego da rede, geralmente a partir de uma porta espelhada (*SPAN port*) de um switch.
* **Analogia:** Um sistema de câmeras de segurança. Ele observa tudo o que acontece, grava as evidências e pode gerar um alarme para um segurança (o analista) quando detecta uma atividade suspeita. No entanto, a câmera não pode intervir fisicamente para parar o intruso.
* **Vantagens:** Como não está no caminho do tráfego, não introduz latência ou jitter na rede. Se o sensor IDS falhar ou ficar sobrecarregado, a rede continua funcionando normalmente.
* **Desvantagens:** Ele é reativo. No momento em que o IDS detecta e alerta sobre um pacote malicioso, esse pacote **já passou** e pode ter atingido seu alvo. Ele não pode parar o ataque em tempo real.

#### **Sistema de Prevenção de Intrusão (IPS)**
* **Modo de Operação:** *Inline* (em linha). Um sensor IPS é posicionado diretamente no caminho do tráfego. Todos os pacotes devem passar *através* do IPS para chegar ao seu destino.
* **Analogia:** Um guarda de segurança posicionado na porta de entrada. Ele inspeciona cada pessoa que tenta entrar e pode **bloquear fisicamente** um indivíduo suspeito, impedindo sua entrada.
* **Vantagens:** Sua principal vantagem é a capacidade de **agir em tempo real**. Ele pode descartar pacotes maliciosos (`drop`), encerrar a conexão (`reset`) ou bloquear o endereço IP do atacante, prevenindo que o ataque seja bem-sucedido.
* **Desvantagens:** Por ser um ponto de passagem obrigatório, ele pode se tornar um gargalo, introduzindo latência. Se o sensor IPS falhar, ele pode interromper todo o tráfego da rede (tornando-se um ponto único de falha).

---

### 2. Como Eles Detectam? Metodologias de Análise

Tanto o IDS quanto o IPS utilizam várias técnicas para identificar atividades maliciosas.

* **Detecção por Assinatura (Signature-Based):** A abordagem mais comum. O sistema possui um vasto banco de dados de "assinaturas", que são padrões únicos correspondentes a ataques conhecidos (ex: um padrão específico de bytes de um exploit, um comando particular de um worm). Ele compara o tráfego de rede com essas assinaturas. É muito eficaz para detectar ameaças conhecidas, mas inútil contra ataques novos (zero-day).
* **Detecção por Anomalia (Anomaly-Based):** O sistema primeiro passa por uma fase de aprendizado para construir uma linha de base (*baseline*) do que é o tráfego "normal" da rede. Depois, ele monitora o tráfego em busca de desvios significativos desse padrão normal. Ele pode detectar ataques desconhecidos, mas é suscetível a gerar *"falsos positivos"* se o comportamento legítimo da rede mudar.
* **Análise de Protocolo (Protocol Analysis):** O sensor usa a definição formal dos protocolos de rede (*RFCs*) para entender como eles *deveriam* funcionar. Ele pode detectar um ataque se um adversário estiver usando um protocolo de forma maliciosa ou não-padrão (ex: usando comandos HTTP inválidos para causar um buffer overflow).

---

### 3. Onde Eles Operam? Tipos de Implementação

* **Baseado em Rede (NIDS/NIPS):** Um sensor NIDS/NIPS é um **dispositivo (físico ou virtual)** posicionado em um ponto estratégico da **rede** para monitorar o tráfego entre múltiplos sistemas. Ele tem uma visão ampla da rede, mas não sabe o que acontece internamente em cada host (especialmente se o tráfego for criptografado).
* **Baseado em Host (HIDS/HIPS):** É um **software** instalado em um **dispositivo final** (um servidor ou uma estação de trabalho). Ele tem uma visão profunda e detalhada daquele host específico, podendo monitorar chamadas de sistema, integridade de arquivos, processos e logs. Um HIPS pode detectar, por exemplo, que um processo do Word está tentando modificar arquivos de sistema, algo que um NIPS não veria. 
* A **combinação de NIPS e HIPS** oferece a melhor cobertura (defesa em profundidade).

---

### 4. O Desafio Operacional: Gerenciando Alertas

A eficácia de um IDS/IPS depende diretamente de sua configuração e do monitoramento humano.

* **Falso Positivo:** O sistema gera um alerta para uma atividade que, na verdade, é legítima. Muitos falsos positivos levam à *"fadiga de alertas"*, onde os analistas podem começar a ignorar alertas importantes.
* **Falso Negativo:** O sistema **falha** em detectar um ataque real. Este é o pior cenário possível.

A tarefa contínua de um analista de segurança é o **"tuning"** do sistema: ajustar as assinaturas e as políticas para maximizar a detecção de ameaças reais (verdadeiros positivos) e minimizar o ruído dos falsos positivos.

### Conclusão

Os sistemas IDS e IPS são componentes vitais da segurança de rede moderna, atuando como um sistema nervoso que detecta ameaças que as defesas de perímetro, como os firewalls, podem não ver. A escolha entre a visibilidade passiva de um IDS e a proteção ativa de um IPS (ou uma combinação de ambos) é uma decisão estratégica baseada nos objetivos de segurança e na tolerância a riscos de uma organização. Em última análise, essas ferramentas não são soluções "instale e esqueça"; elas são sensores poderosos que, quando bem configurados e monitorados por analistas qualificados, fornecem a visibilidade essencial para defender uma rede contra um cenário de ameaças em constante mudança.