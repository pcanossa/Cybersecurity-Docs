# Framework MITRE ATT&CK® - Mapeando o Comportamento do Adversário

## Introdução

No campo da cibersegurança, a capacidade de entender e descrever as ações de um adversário de forma padronizada é crucial para uma defesa eficaz. O Framework MITRE ATT&CK® (Adversarial Tactics, Techniques, and Common Knowledge) surgiu como a resposta a essa necessidade, estabelecendo-se como uma base de conhecimento global e de acesso livre, fundamentada em observações do mundo real.

Diferente de uma simples lista de malwares ou vulnerabilidades, o ATT&CK® foca no **comportamento** do adversário. Ele não descreve a ferramenta que o invasor usa, mas sim *como* ele a utiliza. Funciona como um manual enciclopédico do *modus operandi* dos atores de ameaça, fornecendo uma linguagem comum que permite que profissionais de segurança, ferramentas e organizações falem sobre ameaças de forma clara e precisa.

---

### 1. A Estrutura da Matriz ATT&CK®

O framework é mais conhecido por sua visualização em forma de matriz, que é organizada em três componentes principais: Táticas, Técnicas e Sub-técnicas.

#### **Táticas (Tactics): O "Porquê"**
As táticas representam o **objetivo tático** do adversário em uma determinada fase do ataque. Elas são apresentadas como colunas na matriz e seguem uma ordem lógica que se assemelha ao ciclo de vida de uma intrusão, desde a fase de reconhecimento até o impacto final.

As 14 táticas da matriz Enterprise são:
* Reconnaissance (Reconhecimento)
* Resource Development (Desenvolvimento de Recursos)
* Initial Access (Acesso Inicial)
* Execution (Execução)
* Persistence (Persistência)
* Privilege Escalation (Escalação de Privilégio)
* Defense Evasion (Evasão de Defesa)
* Credential Access (Acesso a Credenciais)
* Discovery (Descoberta)
* Lateral Movement (Movimento Lateral)
* Collection (Coleta)
* Command and Control (Comando e Controle)
* Exfiltration (Exfiltração)
* Impact (Impacto)

#### **Técnicas (Techniques): O "Como"**
As técnicas são as células dentro de cada coluna de tática e descrevem **como** um adversário atinge um objetivo tático. Para cada tática, existem múltiplas técnicas que podem ser empregadas.

* **Exemplo:** Para a tática de **Initial Access**, uma técnica comum é a `T1566: Phishing`.

#### **Sub-técnicas (Sub-techniques): Os "Detalhes do Como"**
As sub-técnicas oferecem um nível de detalhe ainda maior sobre como uma técnica específica é executada.

* **Exemplo:** A técnica `T1566: Phishing` é dividida em sub-técnicas como `T1566.001: Spearphishing Attachment` (Phishing com anexo) e `T1566.002: Spearphishing Link` (Phishing com link).

---

### 2. As Diferentes Matrizes ATT&CK®

O ATT&CK® não é um framework monolítico, mas sim uma coleção de matrizes adaptadas a diferentes domínios tecnológicos:

* **ATT&CK® for Enterprise:** A matriz mais conhecida, focada em ambientes corporativos. Cobre sistemas operacionais (Windows, macOS, Linux) e plataformas de nuvem (Azure AD, Office 365, IaaS).
* **ATT&CK® for Mobile:** Focada em TTPs específicas para sistemas operacionais móveis (Android e iOS).
* **ATT&CK® for ICS (Industrial Control Systems):** Focada nas técnicas únicas usadas para atacar ambientes de Tecnologia Operacional (OT), como redes de energia, fábricas e outras infraestruturas críticas.

---

### 3. A Aplicação Prática do ATT&CK® em Cibersegurança

O verdadeiro poder do ATT&CK® reside em sua aplicação prática nas operações de segurança (SOC - Security Operations Center).

* **Inteligência de Ameaças (Threat Intelligence):** O framework é usado para criar perfis detalhados de atores de ameaça. Em vez de uma descrição vaga, um grupo como o "APT28" pode ser caracterizado pelas técnicas específicas do ATT&CK® que ele utiliza, permitindo uma defesa mais direcionada.

* **Detecção e Caça a Ameaças (Threat Detection & Hunting):** O ATT&CK® impulsiona a mudança de uma defesa baseada em IoCs (Indicadores de Comprometimento) para uma baseada em IoAs (Indicadores de Ataque). Em vez de procurar por um hash de arquivo (que muda facilmente), um analista pode criar uma regra para detectar uma **técnica**, como "alertar sempre que um processo do Microsoft Office gerar um processo filho do PowerShell" (`T1059.001`). Essa detecção comportamental é muito mais resiliente.

* **Emulação de Adversários e Red Teaming:** Equipes de Red Team usam a matriz como um "cardápio" de ataques para simular adversários do mundo real e testar a eficácia das defesas (Blue Team) contra TTPs específicas.

* **Análise de Gaps de Defesa:** As equipes de Blue Team podem mapear suas ferramentas de segurança (EDR, Firewall, SIEM) na matriz ATT&CK® para visualizar quais técnicas possuem boa cobertura e onde existem "pontos cegos" na visibilidade ou proteção.

---

### 4. ATT&CK® vs. Cyber Kill Chain®

É comum comparar o ATT&CK® com o modelo Cyber Kill Chain®, da Lockheed Martin. Eles não são concorrentes, mas sim complementares.

* **Cyber Kill Chain®:** É um modelo de alto nível que descreve as **etapas sequenciais** de um ataque (Reconhecimento, Armamentação, Entrega, etc.). É ótimo para entender o **fluxo** de uma intrusão.
* **MITRE ATT&CK®:** É uma base de conhecimento muito mais granular que descreve as **inúmeras técnicas possíveis** que podem ser usadas *dentro* de cada uma daquelas etapas.

Se a Kill Chain é o índice de um livro, o ATT&CK® é o conteúdo detalhado de todos os capítulos.

### Conclusão

O Framework MITRE ATT&CK® revolucionou a forma como a indústria de cibersegurança opera, criando uma linguagem comum e um modelo de dados aberto para o comportamento do adversário. Ele permite que as organizações evoluam de uma postura reativa, focada em bloquear artefatos de ameaças, para uma estratégia proativa e resiliente, focada em entender, detectar e mitigar as próprias táticas e técnicas dos atacantes. Para o profissional de segurança moderno, a fluência no ATT&CK® não é mais uma opção, mas uma competência essencial.