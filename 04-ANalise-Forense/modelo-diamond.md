# O Modelo Diamond de Análise de Intrusão

## Introdução

Durante e após um incidente de segurança, os analistas são inundados por uma vasta quantidade de dados: endereços IP, hashes de malware, nomes de domínio, contas de usuário comprometidas, etc. O desafio não é apenas coletar esses dados, mas organizá-los de uma forma que revele a narrativa completa do ataque.

O **Modelo Diamond de Análise de Intrusão (The Diamond Model of Intrusion Analysis)** é um framework conceitual projetado para resolver exatamente este problema. Ele fornece um método científico e estruturado para descrever qualquer evento de intrusão, mapeando as relações fundamentais entre os quatro componentes principais de um ataque. Em vez de uma lista de fatos isolados, o modelo constrói um "diamante" de evidências interconectadas, permitindo uma análise mais profunda e a geração de inteligência acionável.

---

### 1. Os Quatro Vértices do Diamante: Os Componentes de um Evento

O modelo postula que todo evento de intrusão pode ser descrito por quatro vértices interligados.

* **Adversário (Adversary):**
    * **Definição:** O "quem". A entidade — seja um indivíduo, grupo ou organização — que é responsável por conduzir o ataque. O objetivo final da análise de atribuição é identificar este vértice com a maior confiança possível.

* **Capacidade (Capability):**
    * **Definição:** O "como". Refere-se a todas as ferramentas, técnicas e exploits utilizados pelo adversário para realizar o ataque.
    * **Exemplos:** Um malware específico (ex: `Emotet`), um exploit para uma vulnerabilidade (ex: `EternalBlue`), ou uma Tática, Técnica e Procedimento (TTP) do framework MITRE ATT&CK (ex: `Phishing`).

* **Infraestrutura (Infrastructure):**
    * **Definição:** O "onde". São os recursos lógicos e físicos que o adversário utiliza para entregar sua capacidade e controlar a operação.
    * **Exemplos:** Endereços IP de servidores de Comando e Controle (C&C), nomes de domínio maliciosos, contas de e-mail usadas para phishing, ou servidores comprometidos usados como pivôs.

* **Vítima (Victim):**
    * **Definição:** O alvo do adversário. A entidade cuja infraestrutura, dados ou pessoal estão sendo atacados.
    * **Exemplos:** A organização, os funcionários (como alvos de engenharia social), os sistemas (servidores, redes) e os ativos de dados.

---

### 2. As Arestas do Diamante: O Poder dos Relacionamentos

A verdadeira genialidade do modelo não está apenas nos vértices, mas nas **arestas** (as linhas que os conectam). Cada aresta representa uma relação fundamental que forma a história do ataque:

* O **Adversário** `usa` uma **Capacidade**...
* ...que é entregue através de uma **Infraestrutura**...
* ...para atingir uma **Vítima**.

Essas conexões são a base para a técnica analítica mais poderosa associada ao modelo: o "pivoting".

---

### 3. O Conceito de "Pivoting": A Aplicação Prática do Modelo

**Pivoting** é a técnica de usar um vértice conhecido do diamante como um ponto de partida para descobrir outros vértices desconhecidos, seguindo as relações entre eles. É o que transforma a análise de estática para dinâmica.

**Exemplo de um Fluxo de Trabalho com Pivoting:**

1.  **Ponto de Partida:** Uma investigação começa com um único Indicador de Comprometimento (IoC). Um analista de SOC encontra um alerta no firewall para uma conexão suspeita com o endereço IP `185.10.59.123`. Este IP é o primeiro vértice conhecido: **Infraestrutura**.

2.  **Primeiro Pivô (Infraestrutura → Capacidade):** O analista insere o IP `185.10.59.123` em uma plataforma de inteligência de ameaças (como VirusTotal). A plataforma informa que este IP é um servidor de C&C conhecido por distribuir o malware bancário **"TrickBot"**. O analista acabou de "pivotar" para o segundo vértice: **Capacidade**.

3.  **Segundo Pivô (Capacidade → Adversário):** O analista agora pesquisa sobre o "TrickBot". Relatórios de inteligência associam este malware a um grupo de cibercrime com motivações financeiras conhecido como **"Wizard Spider"**. O analista pivotou para o terceiro vértice: **Adversário**.

4.  **Terceiro Pivô (Infraestrutura → Outras Vítimas):** Com a infraestrutura identificada (`185.10.59.123`), o analista pode agora buscar em seus logs de rede (NetFlow, logs de proxy) por **outros hosts internos** que também possam ter se comunicado com este IP. Isso pode revelar o escopo completo da infecção dentro de sua própria organização (**Vítima**).

Ao final deste processo, o analista transformou um único endereço IP em um quadro completo, ligando um ator de ameaça específico a uma ferramenta e a um conjunto de vítimas.

---

### 4. Meta-Features: Adicionando Contexto ao Evento

O modelo também inclui "meta-features" que adicionam contexto ao redor do diamante, respondendo a perguntas adicionais sobre o evento:

* **Timestamp:** Quando o evento ocorreu?
* **Fase:** Em qual fase de um modelo como a Cyber Kill Chain® este evento se encaixa?
* **Resultado:** Qual foi o desfecho do evento (sucesso, falha, desconhecido)?
* **Direção:** Qual o sentido do ataque (ex: Adversário-para-Vítima, Vítima-para-Infraestrutura)?

### Conclusão

O Modelo Diamond de Análise de Intrusão fornece um framework simples, porém extremamente poderoso e flexível, para a análise de incidentes. Ao forçar os analistas a estruturarem as evidências em torno dos quatro vértices principais e a explorarem as relações entre eles através do "pivoting", ele transforma peças isoladas de dados em uma narrativa de inteligência coesa. Isso não só ajuda a entender um ataque que já ocorreu, mas também a prever as próximas ações de um adversário e a fortalecer as defesas de forma proativa.