# SHOULDER SURFING AND DUMPSTER DIVING

**Data de Publicação:** 04 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução
Ambos o **Surf de Ombro** e o **Mergulho no Lixo** são táticas clássicas de Engenharia Social. Em vez de explorar falhas em software ou hardware, esses ataques exploram o comportamento humano, seja por desatenção, curiosidade, confiança ou falta de descarte adequado de informações. Eles visam obter dados confidenciais diretamente da fonte humana.

## 1- Surf no Ombro (Shoulder Surfing)
- ***O que é?:** O Surf de Ombro é um ataque onde um invasor fisicamente observa a vítima para obter informações sensíveis. Isso pode ser feito olhando por cima do ombro enquanto a pessoa digita um PIN em um caixa eletrônico, visualiza um código de acesso no celular, ou acessa informações confidenciais em um notebook em local público.
- ***Para que serve / Por que é relevante?:** Este ataque é usado para roubar informações diretamente no momento em que elas são inseridas ou exibidas. Sua relevância está em sua simplicidade e eficácia, pois:
  - Não exige conhecimento técnico avançado.
  - Captura dados em **tempo real** (como PINs e padrões de desbloqueio).
  - **Contorna muitas defesas digitais**, já que a senha não é interceptada, mas sim observada.
- **Como isso acontece?:** O atacante se posiciona discretamente, buscando uma linha de visão clara para a tela ou teclado da vítima.
  - **Proximidade:** Em ambientes movimentados como caixas eletrônicos,cafeterias, aeroportos, ou transporte público.
  - **Tecnologia:** Pode usar binóculos para observar à distância, ou câmeras de segurança (legítimas ou instaladas pelo atacante) para gravar as interações com terminais. 
  A falha é a subestimação do risco e a falta de conscientização da vítima sobre a observação.
- **O que o atacante pode conseguir com isso?:**
  - **Acesso a Contas Financeiras:** PINs, detalhes de cartão de crédito.
  - **Credenciais de Acesso:** Nomes de usuário e senhas para e-mail, redes sociais, sistemas corporativos.
  - **Acesso a Dispositivos:** Padrões de desbloqueio ou PINs de celulares.
- **Ferramentas Utilizadas:**
  - Os próprios **olhos** do atacante.
  - **Dispositivos de gravação** discretos (celulares com câmera, pequenas câmeras espiãs).
  - **Binóculos** para observação à distância.
- **Como se proteger:**
  - **Conscientização:** Esteja sempre ciente do seu entorno, especialmente em locais públicos.
  - **Privacidade Visual:** Ao digitar senhas ou PINs, cubra o teclado com a mão ou o corpo. Posicione sua tela de forma que ela não seja facilmente visível por quem está ao seu redor.
  - **Filtros de Privacidade:** Use películas que restringem o ângulo de visão da tela do seu notebook ou monitor, garantindo que o conteúdo só seja visível para quem está diretamente à frente.
  - **Desconfiança:** Fique atento a pessoas que parecem excessivamente próximas ou que demonstram interesse incomum na sua tela.

### Exemplos de CVE
Como o Shoulder Surfing é uma técnica de ataque físico e de engenharia social, **não existe uma CVE (Common Vulnerabilities and Exposures) diretamente associada a ele**. O Shoulder Surfing explora uma falha de processo ou de conscientização humana, não uma falha em um produto específico.

### CWE Associada
- **CWE-1175: Permissive Access of User Information in Public Displays:** Essa CWE (Common Weakness Enumeration) descreve a fraqueza de permitir que informações sensíveis sejam facilmente visíveis em displays públicos, o que facilita o shoulder surfing.
- **CWE-1033: Inefficient or Insufficient Protection of Credentials:** Mais broadly, a fraqueza de não proteger adequadamente as credenciais, o que inclui métodos de entrada que podem ser observados.

## 2- Mergulho no Lixo (Dumpster Diving)

- ***O que é?:** O Mergulho no Lixo é a prática de examinar o lixo (físico ou digital) de um indivíduo ou organização em busca de informações descartadas que ainda são confidenciais e podem ser usadas em um ataque. A velha frase "O lixo de um homem é o tesouro de outro homem" é perfeita aqui.
- ***Para que serve / Por que é relevante?:** EServe para obter dados que, apesar de descartados, podem ser extremamente valiosos para um atacante. É relevante porque:
  - É uma fonte rica de **informações que burlam defesas digitais** (firewalls, antivírus), pois são documentos físicos ou mídias não destruídas.
  - É uma forma eficaz de **reconhecimento** para planejar ataques de *phishing* ou engenharia social mais convincentes.
  - **Contorna muitas defesas digitais**, já que a senha não é interceptada, mas sim observada.
- **Como isso acontece?:** O atacante literalmente procura em lixeiras, caçambas de lixo, ou áreas de descarte de um alvo.
  - **Locais:**  Lixeiras domésticas, lixeiras de escritórios, centros de reciclagem, ou até mesmo aterros.
  - **Alvos:** Documentos impressos, CDs/DVDs antigos, pendrives, HDDs/SSDs descartados sem formatação segura.
A falha aqui é o descarte inadequado de informações sensíveis, que não foram destruídas de forma irrecuperável.
- **O que o atacante pode conseguir com isso?:**
  - **Credenciais:** Rascunhos de senhas, PINs, códigos de acesso.
  - **Informações de Contato:** Nomes, telefones, e-mails de funcionários, clientes ou fornecedores.
  - **Detalhes Financeiros:** Extratos bancários, faturas, informações de contas.
  - **Dados da Rede/Sistema:** Diagramas de rede, IPs, nomes de servidores, softwares utilizados, manuais.
  - **nformações de Engenharia Social:** Nomes de projetos, estrutura organizacional, dados para *spear phishing* ou fraudes de BEC.
- **Ferramentas Utilizadas:**
  - As **mãos** do atacante.
  - **Sacos de lixo** e luvas.
  - **Conhecimento em engenharia socia** para identificar o valor das informações encontradas.
- **Como se proteger:**
  - **Conscientização:** Esteja sempre ciente do seu entorno, especialmente em locais públicos.
  - **Política de Descarte Seguro:** Todos os documentos confidenciais (pessoais ou corporativos) devem ser **fragmentados (shredded)** usando trituradores de papel (preferencialmente *cross-cut*).
  - **Destruição de Mídias Digitais:** HDDs, SSDs, pendrives, CDs/DVDs antigos devem ser **fisicamente destruídos** (perfuração, desmagnetização, fragmentação) ou ter os dados apagados de forma segura (processo de *wiping*) antes do descarte.
  - **Incineradores:** Para grandes volumes de papel, a incineração é uma opção segura.
  - **Serviços Profissionais:** Contratar empresas especializadas em descarte seguro de informações.
  - **Conscientização:** Educar a si mesmo e a outros sobre a importância de descartar informações corretamente.
  - **Política de Mesa Limpa (Clean Desk Policy):** Não deixar documentos sensíveis expostos em mesas ao sair do local de trabalho.
- 

### Exemplos de CVE
Assim como o Shoulder Surfing, o Dumpster Diving é uma técnica de ataque físico e de engenharia social, e **não possui CVEs diretamente associadas**. O Dumpster Diving explora a falha humana no gerenciamento e descarte de informações.


### CWE Associada
- **CWE-538: Information Exposure Through Debug Log Files (Indirectamente aplicável):** Embora focada em logs digitais, o princípio de vazar informações sensíveis que deveriam ser protegidas se aplica se esses logs forem impressos e descartados sem cuidado.
- **CWE-200: Exposure of Sensitive Information to an Unauthorized Actor:**  Uma CWE mais geral que abrange qualquer forma de exposição de informações sensíveis, incluindo o descarte inadequado que leva ao *dumpster diving*.
- **CWE-1032: Exposure of Private Information:** Similiar à CWE-200, mas com foco específico em informações privadas.























