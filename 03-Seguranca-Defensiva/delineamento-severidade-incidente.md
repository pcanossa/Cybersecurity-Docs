# Delineando a Severidade e a Extensão de um Incidente

## Introdução

Após a coleta inicial de informações em um incidente de segurança, a equipe de resposta (CSIRT) se depara com uma série de dados brutos. Para passar da reação à resposta estratégica, é preciso responder a duas perguntas fundamentais: "Qual o tamanho do problema?" e "Quão grave ele é?".

O processo de **delineamento da severidade e extensão** é a análise crítica que responde a essas perguntas. Ele envolve a avaliação das características técnicas da ameaça e a medição de seu impacto real e potencial nos ativos e operações da empresa. Este processo é o que permite à equipe priorizar suas ações, alocar os recursos corretos e comunicar o risco de forma eficaz para a liderança.

---

### 1. Análise da Ameaça: A Severidade Técnica

Esta fase foca em entender a natureza da exploração ou do malware em si, independentemente do ambiente em que se encontra.

* **Quais são os Requisitos para a Exploração? (Exploitation Requirements)**
    * Esta pergunta avalia a complexidade e as pré-condições do ataque, fatores que influenciam diretamente a probabilidade de sua propagação.
    * **Análise:** O ataque exige interação do usuário (ex: clicar em um link de phishing)? Requer acesso físico ou autenticação prévia? Ou pode ser executado remotamente contra um serviço exposto sem nenhuma autenticação (o pior cenário)? Uma vulnerabilidade que pode ser explorada remotamente com baixa complexidade é inerentemente mais grave.

* **Qual é o Impacto da Exploração? (Exploitation Impact)**
    * Aqui, avaliamos o que o exploit faz ao ser bem-sucedido, geralmente sob a ótica da Tríade CIA (Confidencialidade, Integridade, Disponibilidade).
    * **Análise:** A exploração resulta em uma negação de serviço (**Disponibilidade**)? Permite a modificação não autorizada de dados (**Integridade**)? Ou leva ao vazamento de informações sensíveis (**Confidencialidade**)? O pior caso é uma vulnerabilidade de Execução Remota de Código (RCE), que compromete todos os três pilares.

* **O Exploit está sendo usado "na Selva"? (Is the exploit being used in the wild?)**
    * Existe uma diferença crítica entre uma vulnerabilidade teórica (uma prova de conceito) e uma que está sendo ativamente explorada por grupos de atacantes em campanhas reais.
    * **Análise:** Fontes de inteligência de ameaças (Threat Intelligence) são consultadas para determinar se existem relatos de ataques ativos utilizando este exploit. Uma resposta positiva aumenta drasticamente a urgência da resposta.

* **O Exploit possui Capacidades Semelhantes a um Worm? (Does the exploit have any worm-like capabilities?)**
    * Esta é uma das perguntas mais críticas para a contenção. Um worm é um malware que se propaga automaticamente pela rede, sem interação humana.
    * **Análise:** O malware tem a capacidade de escanear a rede em busca de outros sistemas vulneráveis e se replicar para eles? Um exemplo clássico é o WannaCry, que usou o exploit EternalBlue para se espalhar massivamente. Uma capacidade "wormable" transforma um incidente contido em uma potencial crise em toda a rede e exige medidas de contenção muito mais agressivas e imediatas.

---

### 2. Análise de Escopo: O Impacto no Negócio

Esta fase traduz a severidade técnica em risco para o negócio, avaliando a extensão do comprometimento dentro do ambiente específico da organização.

* **Quantos Sistemas foram Impactados?**
    * Esta é a medida da **amplitude** do incidente. A investigação deve ir além dos sistemas inicialmente reportados.
    * **Análise:** Use os Indicadores de Comprometimento (IoCs) coletados (hashes, IPs, domínios) para varrer toda a rede com ferramentas de EDR e SIEM em busca de outros sistemas infectados. O número de sistemas impactados determina a escala do esforço de limpeza e recuperação.

* **Sistemas Críticos para o Negócio podem ser Afetados? (Can any business-critical systems be affected?)**
    * Esta é a medida da **profundidade** do impacto. Nem todos os sistemas têm o mesmo valor.
    * **Análise:** Identifique os sistemas comprometidos. São estações de trabalho de usuários padrão ou são servidores críticos como Controladores de Domínio, bancos de dados de clientes, servidores de ERP ou sistemas de controle industrial? O comprometimento de um único sistema crítico pode ter um impacto maior do que o de cem estações de trabalho.

* **Qual o Tipo de Dados e Contas em Risco?**
    * A criticidade de um sistema está diretamente ligada aos dados que ele armazena e às contas que o acessam.
    * **Análise:** Os sistemas impactados armazenam dados sensíveis (informações de identificação pessoal - PII, propriedade intelectual, dados financeiros)? O comprometimento envolveu contas de usuários padrão ou contas com privilégios de administrador? A perda de uma conta de Administrador de Domínio é, por si só, um incidente de severidade máxima.

---

### 3. Síntese e Próximos Passos: Da Análise à Ação

A síntese das análises técnica e de escopo permite a formulação de uma estratégia de resposta inicial.

* **Existem Passos de Remediação Sugeridos? (Are there any suggested remediation steps?)**
    * **Análise:** Com base na identificação da vulnerabilidade (CVE) ou do malware, consulte os avisos de segurança dos fornecedores, artigos de inteligência de ameaças e bases de conhecimento.
    * **Ação:** Documente as recomendações, diferenciando entre:
        * **Contenção Imediata:** Ações de curto prazo para parar a hemorragia (ex: isolar o host da rede, bloquear um IP no firewall).
        * **Remediação de Longo Prazo:** Ações para erradicar a causa raiz (ex: aplicar o patch de segurança em toda a empresa, forçar a troca de senhas).

* **Definição da Severidade Geral do Incidente:**
    * Com base em todos os fatores — impacto técnico, capacidades de propagação, número de sistemas e criticidade dos ativos — a equipe atribui um nível de severidade geral ao incidente (ex: Baixo, Médio, Alto, Crítico). Este nível ditará a urgência, os recursos alocados e o nível hierárquico para o qual o incidente deve ser comunicado.

### Conclusão

O delineamento da severidade e da extensão de um incidente é o processo analítico que transforma o "sinal" de um alerta no "mapa" da resposta. Ao avaliar metodicamente as características da ameaça e seu impacto real no ambiente de negócio, a equipe de resposta a incidentes pode sair do modo reativo e tomar decisões estratégicas e priorizadas. Este processo garante que os esforços de contenção e erradicação sejam focados onde eles são mais necessários, minimizando o dano e acelerando a recuperação da organização.