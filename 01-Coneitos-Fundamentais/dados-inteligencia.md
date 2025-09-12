# Dados de Inteligênciade Ameaças Cibernéticas

## Introdução

A Inteligência de Ameaças Cibernéticas (CTI - Cyber Threat Intelligence) é o conhecimento baseado em evidências, incluindo contexto, mecanismos, indicadores, implicações e aconselhamento acionável, sobre uma ameaça ou perigo existente ou emergente para os ativos. No entanto, nem toda inteligência tem o mesmo valor ou longevidade. Os dados de CTI podem ser classificados em uma hierarquia, desde artefatos simples e efêmeros até padrões de comportamento complexos e duradouros. Compreender essa hierarquia é fundamental para construir uma estratégia de defesa que seja tanto reativa em escala quanto proativa e resiliente.

Este artigo explora os três principais tipos de dados de inteligência: Indicadores de Comprometimento (IoCs), Informações de Reputação e as Táticas, Técnicas e Procedimentos (TTPs).

---

### 1. Indicadores de Comprometimento (IoCs)

Os IoCs são as evidências forenses "atômicas" de uma intrusão. São peças de dados estáticos e observáveis que, com alta confiança, indicam que um comprometimento de sistema ou rede *ocorreu*.

* **Definição Técnica:** Um IoC é um artefato observado em um sistema ou rede que pode ser inequivocamente associado a uma atividade maliciosa. Eles são as "impressões digitais" deixadas para trás por um ator de ameaça.

* **Exemplos Comuns:**
    * **Hashes de Arquivo (MD5, SHA256):** A assinatura criptográfica única de um arquivo de malware conhecido.
    * **Endereços IP:** Endereços de servidores de Comando e Controle (C&C), de onde partiu um ataque, ou de sites de phishing.
    * **Nomes de Domínio:** Domínios usados para hospedar malware ou para campanhas de phishing.
    * **Artefatos de Host:** Nomes de arquivos específicos deixados no sistema, chaves de registro do Windows criadas por malware, ou nomes de mutexes.

* **Valor e Limitações:** Os IoCs são a base da detecção automatizada e em escala. Eles são ideais para serem inseridos em listas de bloqueio em firewalls, proxies, gateways de e-mail e plataformas de EDR. No entanto, seu valor é **tático e de curta duração**. Um atacante pode facilmente compilar uma nova versão de seu malware (gerando um novo hash), alugar um novo servidor (obtendo um novo IP) ou registrar um novo domínio, tornando os IoCs antigos obsoletos.

---

### 2. Informações de Reputação

A inteligência de reputação é uma avaliação da "bondade" ou "maldade" de um objeto da internet (IP, domínio, URL), baseada em seu comportamento histórico e contexto. É uma forma de inteligência agregada e preditiva.

* **Definição Técnica:** É uma pontuação de risco ou categorização atribuída a um destino da internet, derivada da análise contínua de fontes de dados massivas e globais (como tráfego de e-mail, logs de proxy, etc.).

* **Como Funciona:** Em vez de uma correspondência exata (como em um IoC), a reputação funciona com base em probabilidades e padrões.
    * Um endereço IP que foi observado enviando spam nos últimos 30 dias terá uma **reputação de e-mail ruim**.
    * Um domínio que foi registrado há menos de 24 horas terá uma **reputação suspeita**.
    * Uma URL que usa técnicas de ofuscação e redirecionamento terá uma **reputação de web arriscada**.

* **Valor e Aplicação:** A reputação permite a tomada de decisões de segurança baseadas em risco. Um e-mail de um remetente com reputação ruim pode ser colocado em quarentena para análise, enquanto um e-mail de uma fonte com reputação comprovadamente maliciosa pode ser bloqueado instantaneamente. É um componente essencial de gateways de segurança modernos.

---

### 3. Táticas, Técnicas e Procedimentos (TTPs)

Os TTPs são o nível mais alto e mais valioso de inteligência de ameaças. Eles não descrevem os artefatos de um ataque, mas sim o **comportamento do adversário**.

* **Definição Técnica:** Descrevem o *modus operandi* de um ator de ameaça.
    * **Táticas:** O objetivo tático de alto nível (ex: Acesso Inicial, Movimento Lateral, Exfiltração).
    * **Técnicas:** O método específico usado para alcançar uma tática (ex: Phishing, Uso de PowerShell).
    * **Procedimentos:** A implementação detalhada e passo a passo de uma técnica por um ator de ameaça específico.

* **O Framework MITRE ATT&CK®:** É a base de conhecimento global e o padrão de fato para catalogar e descrever as TTPs dos adversários.

* **Valor e Aplicação:** A inteligência de TTPs é **estratégica e duradoura**. Enquanto um atacante pode mudar seus IoCs (ferramentas e infraestrutura) com facilidade, mudar seu comportamento fundamental (suas TTPs) é extremamente difícil, custoso e demorado. As defesas baseadas na detecção de TTPs — como regras de EDR que alertam quando o `winword.exe` gera um processo `powershell.exe` — são muito mais resilientes e eficazes contra ataques novos e desconhecidos.

---

### A Pirâmide da Dor

O conceito da "Pirâmide da Dor" organiza esses tipos de inteligência com base em quão "doloroso" é para um atacante ter aquele indicador bloqueado pela defesa.

* **Base da Pirâmide (Pouca Dor):** `Hashes`, `Endereços IP`, `Nomes de Domínio`. Fáceis de bloquear, mas também triviais para o atacante mudar.
* **Topo da Pirâmide (Muita Dor):** `TTPs`. Detectar e bloquear o comportamento de um atacante o força a reaprender e a desenvolver novas metodologias, o que é um grande obstáculo.

A inteligência de reputação se situa no meio, sendo mais valiosa que IoCs atômicos, mas menos resiliente que a detecção de TTPs.

### Conclusão

Uma operação de segurança madura utiliza todos os níveis da hierarquia de inteligência. Os **IoCs** e os dados de **Reputação** são essenciais para a defesa automatizada em escala, bloqueando a grande maioria das ameaças conhecidas no perímetro. As **TTPs**, por outro lado, são a base para a construção de defesas resilientes e para a condução de atividades proativas de *Threat Hunting*, permitindo que os analistas procurem pelo *comportamento* do adversário, e não apenas pelas suas ferramentas. Entender essa hierarquia permite que uma organização evolua de uma postura puramente reativa para uma estratégia de defesa preditiva e estratégica.