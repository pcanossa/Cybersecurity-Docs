# ENGENHARIA SOCIAL

**Data de Publicação:** 05 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução
Engenharia Social é uma **estratégia não-técnica** (ou seja, não explora falhas de software ou hardware) que visa **manipular indivíduos** (seres humanos) para que realizem certas ações ou divulguem informações confidenciais. 

## O que é?
É a arte de enganar pessoas para que elas, voluntariamente (mesmo que sem saber), comprometam a própria segurança ou a segurança da organização em que trabalham.
Em vez de focar em vulnerabilidades de sistemas, a engenharia social explora a natureza humana, aproveitando-se de características:
- **Desejo de Ajuda:** As pessoas geralmente querem ser úteis e solícitas.
- **Confiança:** Tendência a confiar em figuras de autoridade ou em quem parece estar em apuros.
- **Curiosidade:**  O desejo de saber mais, especialmente sobre ofertas ou problemas urgentes.
- **Medo/Urgência** A pressão para agir rapidamente para evitar uma consequência negativa.
- **Ganância/Vaidade:**  A tentação por recompensas ou a busca por reconhecimento.
Em suma, a Engenharia Social é a arte de transformar um ser humano em uma vulnerabilidade ativa, muitas vezes sem que ele perceba que está sendo manipulado.


## Qual sua relevância?

A Engenharia Social é uma das táticas mais perigosas e eficazes no arsenal de um atacante, e sua relevância é enorme no cenário atual de cibersegurança.
Ela é crucial porque:
- **É o Vetor de Ataque Inicial mais Comum:** Muitos dos ataques cibernéticos mais complexos e devastadores (como ransomware em empresas, grandes vazamentos de dados, fraudes financeiras) **começam com um golpe de engenharia social**. É a "porta de entrada" que leva a outros tipos de exploração.
- **Contorna Defesas Tecnológicas:** Por focar no elemento humano, a Engenharia Social pode **burlar *firewalls*, antivírus, sistemas de detecção de intrusão e até mesmo autenticação multifator**, pois a própria vítima é induzida a fornecer as informações ou acesso.
- **Alto Retorno sobre o Investimento:** Não exige ferramentas ou conhecimentos técnicos caros, apenas criatividade, pesquisa e **habilidade de manipulação**.
- **Diversidade de Ataques:** Pode ser usada para:
  - Roubar **credenciais** (senhas, PINs).
  - Instalar **malware** (Fazendo a vítima abrir um anexo ou um arquivo baixado).
  - Obter **acesso físico** a instalações.
  - Induzir **fraudes financeiras** (ex: fraudes de CEO).
  - Coletar **informações confidenciais** (dados de clientes, projetos, segredos comerciais).

## Como acontece?
Conceitualmente, a Engenharia Social funciona criando um cenário de **engano crível** que leva a vítima a agir contra seus próprios interesses de segurança.
Os passos típicos de um ataque de Engenharia Social incluem:
1. **Reconhecimento (Reconnaissance):**  O atacante coleta o máximo de informações possível sobre a vítima ou a organização alvo. Isso pode incluir nomes de funcionários, cargos, estrutura da empresa, fornecedores, hobbies, detalhes de projetos, tecnologias usadas, e-mails, números de telefone. (Técnicas como [*Shoulder Surfing, Dumpster Diving*](./shoulder_surfing_e_dumpster_diving.md), pesquisa em redes sociais como *LinkedIn* são usadas aqui).
2. **Preparação da Isca:** Com base nas informações coletadas, o atacante cria uma "história" ou "motivo" convincente. Ele pode se passar por uma figura de autoridade (TI, CEO, segurança), um colega, um fornecedor, ou até mesmo um técnico de suporte. O artefato do ataque (e-mail, mensagem de texto, ligação, site falso) é cuidadosamente elaborado para ser autêntico.
3. **Abordagem (Pretexting/Phishing/Vishing):**  O atacante faz contato com a vítima.
    - **Pretexting:** Cria um cenário falso (um pretexto) para enganar a vítima a divulgar informações (ex: "Sou do suporte técnico e preciso da sua senha para resolver um problema crítico no seu computador").
    - **Phishing:** Envia comunicações fraudulentas em massa (e-mails, mensagens) que parecem legítimas para roubar credenciais ou instalar malware.
    - **Vishing:** Phishing por voz, usando chamadas telefônicas falsas.
    - **Smishing:** Phishing por SMS.
    - **Impersonificação:** Fisicamente se passar por alguém (ex: técnico de manutenção, entregador) para obter acesso.
4. **Execução da Manipulação:**  O atacante usa táticas psicológicas para pressionar a vítima a agir:
    - **Senso de Urgência:** "Faça isso agora ou sua conta será bloqueada!"
    - **Autoridade:** "O CEO pediu isso, é urgente!"
    - **Medo:** "Se você não clicar, seu computador será infectado!"
    - **Curiosidade/Recompensa:** "Você ganhou um prêmio, clique aqui para resgatar!"
5. **Coleta de Informação/Execução da Ação:**  A vítima, manipulada, realiza a ação desejada pelo atacante (clica em um link, abre um anexo, divulga uma senha, transfere dinheiro, concede acesso físico).
6. **Saída:** O atacante se retira discretamente, muitas vezes deixando a vítima sem saber que foi enganada.

## Como funciona na prática (Exemplo)
Vamos usar um exemplo prático de um ataque de **Business Email Compromise (BEC)**, que é uma forma sofisticada de Engenharia Social.
**Cenário:** Um atacante quer que o departamento financeiro de uma empresa transfira dinheiro para uma conta fraudulenta.
1. **Reconhecimento:** O atacante pesquisa a empresa-alvo, identifica o CEO (ou um alto executivo) e o chefe do departamento financeiro. Ele coleta informações sobre a estrutura de e-mails da empresa, nomes de fornecedores, projetos em andamento, etc., muitas vezes através de redes sociais (*LinkedIn*), site da empresa, ou até mesmo *dumpster diving*.
2. **Criação de Pretexto:** O atacante cria um endereço de e-mail muito parecido com o do CEO (ex: ceo@empresa.com vira ceo@eempresa.com ou ceo.empresa@gmail.com com um "display name" de "CEO Nome Sobrenome").
3. **Abordagem (Email Fraudulento):**  O atacante envia um e-mail urgente para o chefe do financeiro, vindo do e-mail falso do "CEO".
    - **Assunto:** "Transferência URGENTE - Aquisição Secreta"
    - **Corpo do Email:** "Olá [Nome do Chefe do Financeiro], estou em uma viagem de negócios muito importante e preciso que você faça uma transferência confidencial IMEDIATA para um novo fornecedor. Este projeto é de altíssima prioridade e sensibilidade. Os detalhes da conta estão anexados/abaixo. Não ligue para meu telefone; estou em uma reunião crucial. Confio em você para agilizar isso."
    - **Assinatura:** Assinatura padrão utilizada pelo CEO em emails.
4. **Execução da Manipulaçao:** 
    - **Autoridade:** O e-mail parece vir do CEO.
    - **Urgência:**  "IMEDIATA", "altíssima prioridade", "reunião crucial".
    - **Medo/Pressão:** A implicação de que o chefe do financeiro deve agir sem questionar para não prejudicar um "projeto secreto".
    - **Restrição de Verificação:** "Não ligue para meu telefone".
5. **Fraude Financeira:** O chefe do financeiro, sob pressão e acreditando que é o CEO, processa a transferência para a conta bancária do atacante, sem verificar por um canal secundário.
6. **Saída:** O dinheiro é transferido, e o atacante desaparece. A fraude pode levar dias para ser descoberta.

## O que o atacante pode conseguir com isso?
As consequências da Engenharia Social são vastas e podem ser catastróficas:
- **Fraudes Financeiras:** Indução de transferências de dinheiro (BEC), compras não autorizadas.
- **Roubo de Credenciais:** Acesso a contas bancárias, e-mail, sistemas corporativos, redes sociais.
- **Instalação- de Malware:** Ransomware, spyware, keyloggers no dispositivo da vítima ou na rede da empresa.
- **Acesso Físico Não Autorizado:** Entrar em instalações restritas.
- **Vazamento de Dados:** Roubo de informações confidenciais de clientes, propriedade intelectual, segredos comerciais.
- **Roubo de Identidade:** Obtenção de informações pessoais para cometer crimes em nome da vítima.
- **Manipulação de Lógica de Negócio:** Alterar processos, redirecionar entregas, etc.

## Ferramentas utilizadas
As ferramentas para Engenharia Social são diversas e focam em facilitar a criação de enganos e a comunicação com as vítimas:
- **Ferramentas de Reconhecimento/OSINT:**
    - **Redes Sociais:** LinkedIn, Facebook, Instagram para coletar informações pessoais e profissionais.
    - **Websites Corporativos:** Para entender a estrutura da empresa, nomes de funcionários, eventos.
    - **Motores de Busca (Google Dorking):** Para encontrar informações expostas.
    - **Shodan/Censys:** Para encontrar informações sobre a infraestrutura da empresa.
- **Ferramentas de Phishing/Simulação:**
    - **GoPhish, EvilGinx, KingPhish:** Plataformas para criar e gerenciar campanhas de *phishing* e *vishing*, clonar sites, e coletar credenciais.
    - **HTTrack/Wget:** Para clonar páginas web legítimas.
- **Serviços de Comunicação:**
    - **Serviços de E-mail/SMS:** Para enviar as iscas.
    - **Ferramentas de *Spoofing*:**  Para falsificar números de telefone ou endereços de e-mail remetentes.
- **Registro de Domínios:** Registrar domínios semelhantes aos legítimos (*typosquatting*).
- **Kits de Engenharia Social:** Pacotes prontos (às vezes com código malicioso) vendidos em fóruns criminosos.
- **Ferramentas de Disfarce e Impersonificação:** Roupas, crachás falsos, veículos com logos falsos (para ataques físicos).

## Como mitigar
A mitigação contra Engenharia Social é a mais desafiadora, pois depende do fator humano. É uma defesa em múltiplas camadas:
- **Educação e Conscientização (A Defesa MAIS CRÍTICA):** Treinamento contínuo para todos os indivíduos (funcionários, usuários) sobre:
    - **Como identificar Phishing, Vishing e Smishing:** Verificar remetentes, links, erros de gramática, senso de urgência.
    - **Desconfiança:** Desenvolver um ceticismo saudável em relação a solicitações incomuns ou urgentes.
    - **Verificação Independente:** Sempre verificar solicitações de informações ou ações importantes por um canal de comunicação diferente e independente (ex: ligar para um número oficial da empresa, não para o número dado no e-mail suspeito).
    - **Não Divulgar Informações Pessoais/Corporativas Inesperadamente:** Nunca fornecer senhas ou dados confidenciais por e-mail, SMS ou telefone, a menos que se tenha iniciado a comunicação e verificado a autenticidade.
- **Políticas de Segurança Robustas:**
    - **Política de Mesa Limpa:** Não deixar documentos sensíveis expostos.
    - **Política de Descarte Seguro:** Fragmentar documentos, destruir mídias digitais.
    - **Controle de Acesso Físico:** Portaria, crachás, autenticação para áreas restritas.
- **Tecnologia de Suporte:** Embora a Engenharia Social não seja puramente técnica, a tecnologia pode ajudar a reduzir as oportunidades para o atacante:
    - **Autenticação Multifator (MFA/2FA):** Mesmo que uma senha seja roubada, o MFA impede o acesso não autorizado.
    - **Filtros de Spam e Gateways de Segurança de E-mail (SEG):** Para bloquear e-mails de phishing e malware.
    - **DMARC, SPF, DKIM:** Para detectar spoofing de domínio em e-mails.
    - **Navegadores com Proteção Anti-Phishing:**  Alertam sobre sites maliciosos conhecidos.
    - **Soluções de EDR/Antivírus:** Para detectar e bloquear malware caso a vítima caia na isca.
    - **Uso de Contas de Privilégio Mínimo:**  Limitar o poder que um usuário tem, para que, mesmo que sua conta seja comprometida, o dano seja contido.

## Como isso aparece em Threat Intelligence
A Engenharia Social é onipresente em relatórios de Threat Intelligence, sendo um dos pilares de quase todas as operações de cibersegurança, desde ataques simples a campanhas de APT de alto nível.
- **Vetor de Ataque Inicial Dominante:** Relatórios anuais de segurança consistentemente mostram a Engenharia Social (especialmente Phishing) como o principal vetor para ransomware, vazamentos de dados e fraudes.
- **Temas e Táticas em Evolução:** A inteligência de ameaças rastreia as tendências nos "ganchos" usados por engenheiros sociais (pandemias, eventos globais, novas tecnologias) e as técnicas de evasão para burlar defesas de e-mail.
- **Grupos APT e Espionagem:** Muitos dos grupos *APT* (Advanced Persistent Threats) mais sofisticados utilizam Spear Phishing e Vishing altamente direcionados e pesquisados como a fase inicial para obter acesso a redes governamentais, militares ou de alta tecnologia.
- **Cibercrime Organizado:** Grupos de ransomware e fraudes financeiras dependem pesadamente da Engenharia Social para comprometer as organizações. Ataques de BEC (Business Email Compromise), que são uma forma de Engenharia Social, resultam em bilhões de dólares em perdas anualmente.
- **Detecção de Infraestrutura Adversária:** A Threat Intelligence também se concentra na identificação de domínios falsos, servidores de comando e controle, e infraestruturas de phishing usadas em campanhas de Engenharia Social.

## Aparece em MITRE ATT&CK como:
No MITRE ATT&CK, a Engenharia Social é uma técnica crucial na tática de **Acesso Inicial (Initial Access)**, mas também pode aparecer em outras táticas, como **Persistência** ou **Coleta**, dependendo de como a manipulação é usada.
- **TA0001 - Initial Access:** Esta é a tática onde o impacto da Engenharia Social é mais visível, pois é a forma como os adversários obtêm o primeiro ponto de apoio na rede.
    - **T1566 - Phishing:** A técnica mais comum. Abrange e-mails com links ou anexos maliciosos (Spearphishing Attachment, Spearphishing Link), e phishing via outros serviços (redes sociais).
    - **T1566.004 - Phishing for Information:**  Especificamente para enganar a vítima a divulgar informações sensíveis (fora credenciais de login diretas).
    - **T1078 - Valid Accounts:**  Embora não seja uma técnica de engenharia social por si só, o objetivo de muitas técnicas de engenharia social é obter contas válidas para o adversário, permitindo acesso autêntico.
    - **T1078.003 - Local Accounts (com contexto de engenharia social):** Se um engenheiro social convence alguém a criar uma conta local para ele.
    - **T1583 - Acquire Infrastructure:** Em casos de engenharia social em fornecedores de nuvem, por exemplo, para adquirir infraestrutura para o atacante.
- **TA0003 - Persistence:** Se o engenheiro social convence a vítima a instalar um backdoor ou a manter um acesso (por exemplo, "deixe esta ferramenta de acesso remoto instalada para futuras manutenções"), isso se enquadra em persistência.
- **TA0009 - Collection:** As técnicas de **Shoulder Surfing** (T1589.002 - Gather Victim Identity Information: Credentials) e **Dumpster Diving** (T1592 - Gather Victim Host Information, T1594 - Gather Victim Org Information) são classificadas sob a tática de **Reconnaissance**, que se traduz em coleta de informações.

## Conclusão
A Engenharia Social sublinha a importância de uma defesa em profundidade que não ignore o "fator humano". Por mais robustos que sejam os sistemas tecnológicos, uma única falha de atenção pode ser a brecha que um atacante precisa.






















































