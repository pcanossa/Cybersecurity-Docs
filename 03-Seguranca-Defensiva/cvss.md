# CVSS - Quantificando a Severidade de Vulnerabilidades

## Introdução

Todos os dias, novas vulnerabilidades de software são descobertas e divulgadas publicamente, cada uma recebendo um identificador único (um CVE). Para uma equipe de segurança, que pode lidar com centenas ou milhares de vulnerabilidades em sua rede, a pergunta mais crítica é: "Qual delas devemos corrigir primeiro?".

O **Common Vulnerability Scoring System (CVSS)** foi criado para responder a essa pergunta. Ele é um framework aberto e padronizado, mantido pelo FIRST.org, que fornece um método transparente para comunicar as características e calcular a severidade de uma vulnerabilidade. O resultado é uma pontuação numérica de 0.0 (nenhum risco) a 10.0 (risco crítico), que permite às organizações priorizar seus esforços de remediação de forma objetiva e baseada em dados.

---

### 1. A Anatomia de uma Pontuação CVSS: Os Três Grupos de Métricas

Uma pontuação CVSS não é um número subjetivo; ela é calculada a partir de três grupos de métricas, cada um com um propósito diferente.

#### **Métricas Base (Base Metrics)**
Este grupo representa as **características intrínsecas e imutáveis** da vulnerabilidade em si. Essa é a pontuação que você geralmente vê associada a um CVE em bancos de dados públicos, e ela não muda com o tempo ou dependendo do ambiente.

As métricas base são divididas em:

* **Vetor de Ataque (Attack Vector - AV):** Como a vulnerabilidade pode ser explorada?
    * `Network (N)`: Remotamente, pela internet. (Pior)
    * `Adjacent (A)`: O atacante precisa estar na mesma rede local (LAN, Wi-Fi, Bluetooth).
    * `Local (L)`: O atacante precisa de acesso local ao sistema (ex: teclado) ou já ter uma conta de usuário.
    * `Physical (P)`: O atacante precisa de acesso físico ao dispositivo. (Menos grave)

* **Complexidade do Ataque (Attack Complexity - AC):** Quão difícil é para o atacante explorar a falha?
    * `Low (L)`: Não existem obstáculos; o ataque é direto.
    * `High (H)`: O atacante precisa superar condições fora de seu controle (ex: vencer uma condição de corrida, ou enganar um usuário em uma situação muito específica).

* **Privilégios Requeridos (Privileges Required - PR):** O atacante precisa estar autenticado no sistema para atacar?
    * `None (N)`: Não é necessária nenhuma autenticação. (Pior)
    * `Low (L)`: O atacante precisa de privilégios de um usuário comum.
    * `High (H)`: O atacante precisa de privilégios de administrador.

* **Interação do Usuário (User Interaction - UI):** A exploração exige que um usuário legítimo participe?
    * `None (N)`: Não, o ataque pode ser executado sem nenhuma interação.
    * `Required (R)`: Sim, o atacante precisa que a vítima clique em um link, abra um arquivo, etc.

* **Escopo (Scope - S):** A exploração da vulnerabilidade pode afetar componentes além do componente vulnerável?
    * `Changed (C)`: Sim. Uma vulnerabilidade em uma máquina virtual que permite ao atacante escapar e executar código no sistema hospedeiro é um exemplo de mudança de escopo. (Pior)
    * `Unchanged (U)`: Não, o impacto fica contido no mesmo componente.

* **Impacto (na Tríade CIA):** Qual o dano à **Confidencialidade (C)**, **Integridade (I)** e **Disponibilidade (A)** do sistema?
    * `High (H)`: Perda total.
    * `Low (L)`: Perda parcial.
    * `None (N)`: Nenhum impacto.

#### **Métricas Temporais (Temporal Metrics)**
Este grupo reflete características da vulnerabilidade que **mudam com o tempo**. Elas permitem ajustar a pontuação base para cima ou para baixo.

* **Maturidade do Código de Exploit (Exploit Code Maturity - E):** Já existe um exploit funcional para essa falha? (Uma falha com um exploit público é mais perigosa).
* **Nível de Remediação (Remediation Level - RL):** Já existe uma correção oficial? (A existência de um patch oficial reduz a urgência).
* **Confiança do Relatório (Report Confidence - RC):** Qual a certeza de que a vulnerabilidade é real e seus detalhes estão corretos?

#### **Métricas Ambientais (Environmental Metrics)**
Este é o grupo mais importante para a **priorização interna** de uma organização. Ele permite que a equipe de segurança personalize a pontuação para o **seu ambiente específico**.

* **Requisitos de Segurança (CR, IR, AR):** Qual a importância da Confidencialidade, Integridade e Disponibilidade para o **ativo específico** que está vulnerável na *minha* rede? (Uma vulnerabilidade de negação de serviço tem um impacto muito maior em um servidor web de produção do que em uma estação de trabalho de um estagiário).
* **Métricas Base Modificadas:** A organização pode reavaliar as métricas base para seu contexto. Por exemplo, se uma vulnerabilidade tem um Vetor de Ataque "Network", mas o servidor vulnerável está em uma rede interna, segmentada e sem acesso à internet, a equipe pode modificar o vetor para "Adjacent", reduzindo a pontuação final para seu ambiente.

---

### 2. A Pontuação Final e as Classificações de Severidade

Após a análise das métricas, uma calculadora CVSS gera uma pontuação final que se enquadra em uma escala de severidade padrão:

| Pontuação | Nível de Severidade |
| :--- | :--- |
| **9.0 - 10.0** | **Crítica (Critical)** |
| **7.0 - 8.9** | **Alta (High)** |
| **4.0 - 6.9** | **Média (Medium)** |
| **0.1 - 3.9** | **Baixa (Low)** |
| **0.0** | **Nenhuma (None)** |

---

### 3. Como Usar o CVSS na Prática

* **Triagem de Vulnerabilidades:** Uma varredura de vulnerabilidades pode retornar milhares de resultados. A equipe de segurança usa a **Pontuação Base** do CVSS para fazer a triagem inicial, ordenando as vulnerabilidades da mais crítica para a mais baixa e focando os esforços de correção no topo da lista.
* **Contextualização para Priorização:** Uma organização madura não para na pontuação base. Ela aplica as **Métricas Ambientais** para entender o risco real para o seu negócio. Uma vulnerabilidade "Média" em um servidor de banco de dados crítico pode ser mais prioritária do que uma "Crítica" em um quiosque de informações isolado.
* **Comunicação:** O CVSS fornece uma linguagem comum e objetiva para discutir riscos. Permite que as equipes de segurança comuniquem a severidade das vulnerabilidades para as equipes de TI e para a gestão de forma padronizada e baseada em dados.

### Conclusão

O CVSS é um framework indispensável para a prática moderna de gestão de vulnerabilidades. Ele transforma o que poderia ser um processo caótico e subjetivo em uma análise estruturada e transparente. Ao fornecer uma pontuação padronizada, ele permite que as organizações priorizem de forma inteligente seus recursos limitados, garantindo que as falhas de segurança mais perigosas para o seu ambiente específico sejam corrigidas primeiro.