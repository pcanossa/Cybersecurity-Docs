# Análise de Incidente: Campanha de Vishing e Extorsão Direcionada a Ambientes SaaS (Scattered Spider)

**Data de Publicação:** 14 de agosto de 2025  
**Nível de Ameaça:** Crítico 
**Autor:** Patrícia Canossa (com base em relatório do Google Cloud / Mandiant)

---

### 1. Resumo Executivo

Em junho de 2024, analistas do Google Cloud e da Mandiant detalharam uma campanha de ciberataques em andamento, atribuída ao grupo de ameaça `UNC3944` (também conhecido como **Scattered Spider** atualmente) . A campanha utiliza uma abordagem multifacetada que começa com *Vishing* (Phishing por Voz) para enganar funcionários de help desk e obter acesso inicial. Subsequentemente, os atacantes se movem lateralmente, abusam de ferramentas legítimas e exfiltram dados de plataformas **SaaS** (Software as a Service), como *Salesforce* e *Microsoft 365*, para depois extorquir as vítimas. O sucesso da campanha reside na manipulação de pessoas e processos, em vez da exploração de vulnerabilidades de software.

### 2. Organização Afetada e Alvo

* **Setor:** Múltiplos, com foco em grandes corporações.
* **Localização:** Global, com ênfase em filiais de língua inglesa de empresas multinacionais.
* **Alvo Principal:** Funcionários de TI e suporte técnico (help desk) e, por consequência, as plataformas SaaS da organização, especialmente *Salesforce* e ambientes *Okta/Microsoft 365*.

O grupo `UNC3944` demonstra um profundo conhecimento dos processos de suporte de TI corporativos. Eles visam organizações com grandes equipes de suporte, muitas vezes terceirizadas, que são mais suscetíveis a táticas de engenharia social devido à natureza de seu trabalho de atendimento.

### 3. Vulnerabilidade Explorada: O Fator Humano (CWE-300)

* **Identificador:** Não aplicável (N/A) - O ataque não explora uma vulnerabilidade de software específica (CVE).
* **Sistema Afetado:** Processos de suporte de TI e conscientização de segurança dos funcionários.
* **Tipo de Falha (CWE-300):** Violação de Canal ou Caminho (*Channel Accessible by Non-Endpoint*). Neste contexto, refere-se à manipulação de canais de comunicação legítimos (telefone, SMS) para contornar controles de segurança.
* **Impacto:** Acesso inicial à rede, roubo de credenciais, exfiltração de dados e extorsão financeira.
* **Status da Correção:** Requer melhoria contínua de processos e treinamento de pessoal.

#### Detalhamento Técnico do Vetor de Ataque

A "vulnerabilidade" central é o fator humano. Os atacantes não precisam de um *zero-day*. Eles exploram a disposição humana em ajudar, especialmente em um contexto de suporte técnico.

O ataque se baseia na capacidade do ator de se passar por um funcionário legítimo que precisa de ajuda urgente. Eles reúnem informações sobre a vítima (nome, cargo, etc.) a partir de fontes públicas (como o *LinkedIn*) para tornar a chamada de Vishing mais convincente. O objetivo é persuadir o analista de suporte a:
1. Redefinir uma senha.
2. Gerar um código de Autenticação Multifator (MFA) temporário.
3. Instruir o "usuário" (o atacante) a instalar uma ferramenta de acesso remoto "aprovada" pela empresa.

Uma vez que o atacante obtém as credenciais e supera o MFA com a ajuda do próprio funcionário, a segurança do perímetro é efetivamente violada.

### 4. Metodologia do Ataque (Cadeia de Ataque)

A campanha segue um padrão claro e bem definido.

**Fase 1: Reconhecimento e Preparação**

* O grupo `UNC3944` seleciona uma organização alvo e coleta informações sobre seus funcionários, especialmente os de TI, a partir de redes sociais profissionais.
* Eles identificam os processos de suporte da empresa e as ferramentas de acesso remoto utilizadas.

**Fase 2: Acesso Inicial via Vishing**

* O atacante realiza uma chamada de Vishing para o help desk da vítima, se passando por um funcionário.
* Com urgência e pretextos convincentes (ex: "esqueci meu token MFA em casa e preciso acessar um relatório para uma reunião agora"), ele convence o analista a redefinir credenciais e/ou fornecer um bypass de MFA.

**Fase 3: Implantação de Ferramentas e Persistência**

* Com acesso à conta do usuário, o atacante instala ferramentas legítimas de gerenciamento e acesso remoto (*SplunkRMM - Remote Management and Monitoring*). Isso permite que eles mantenham o acesso mesmo que a senha da vítima seja alterada posteriormente.
* Eles utilizam essas ferramentas para se aprofundar na rede e entender o ambiente.

**Fase 4: Movimentação Lateral e Acesso a Dados SaaS**

* O atacante busca por credenciais salvas, especialmente para plataformas SaaS críticas.
* Uma vez que obtêm acesso a uma conta do *Salesforce*, por exemplo, eles realizam consultas para entender a estrutura dos dados.
* Iniciam a exfiltração de dados em pequenos blocos para evitar a detecção por ferramentas de monitoramento que buscam grandes volumes de download.

**Fase 5: Extorsão**

* Após a exfiltração bem-sucedida, os atacantes contatam a organização.
* Eles enviam e-mails ou fazem chamadas para funcionários, exigindo um pagamento (geralmente em Bitcoin) dentro de um prazo curto (ex: 72 horas) para evitar o vazamento dos dados roubados.

### 5. Análise do Grupo de Ameaça: `UNC3944` / Scattered Spider

Este grupo é conhecido por sua alta proficiência em engenharia social e por operar com um ritmo muito rápido, sobrecarregando as equipes de resposta a incidentes.

**Principais Táticas, Técnicas e Procedimentos (TTPs):**

* **Engenharia Social:** Uso massivo de Vishing e Smishing (Phishing por SMS).
* **Abuso de Identidade:** Especializados em contornar o MFA através da manipulação de pessoas e processos, não da tecnologia em si.
* **Living off the Land (LotL):** Utilizam softwares legítimos e aprovados pela vítima (como ferramentas de RMM) para se misturar ao tráfego normal e evitar a detecção.
* **Foco em SaaS:** Compreendem que os dados mais valiosos de uma empresa (clientes, finanças, PII) estão frequentemente em plataformas como *Salesforce*, *Workday* e *Microsoft 365*.
* **Operações Rápidas:** Desde o acesso inicial até a exfiltração de dados, suas ações podem ocorrer em questão de horas ou poucos dias.

### 6. Mitigação e Recomendações

Como o ataque se concentra em pessoas e processos, as mitigações devem ser igualmente focadas nesses pilares.
1. **Fortalecimento do Help Desk:**
    * Implementar procedimentos de verificação de identidade mais rigorosos para solicitações de redefinição de senha e **MFA**. Por exemplo, exigir uma chamada de vídeo ou a aprovação de um gerente para ações sensíveis.
    * **Treinar** continuamente as equipes de suporte para reconhecer táticas de engenharia social e pressão psicológica.
2. **MFA Resistente a Phishing:**
    * Adotar soluções de **MFA** baseadas em *FIDO2/WebAuthn*, que vinculam a autenticação ao hardware físico (como chaves de segurança *YubiKey*) e são resistentes a ataques de phishing e *adversary-in-the-middle*.
3. **Monitoramento de SaaS:**
    * Utilizar ferramentas de **SaaS Security Posture Management (SSPM)** para monitorar comportamentos anômalos, como logins de locais incomuns, aumento súbito no volume de consultas de API ou exfiltração de dados, mesmo em pequenos blocos.
4. **Princípio do Menor Privilégio:**
    * Garantir que as contas de usuário tenham acesso apenas aos dados e aplicativos estritamente necessários para suas funções. Isso limita o "raio de explosão" caso uma conta seja comprometida.
5. **Cultura de Segurança:**
    * Promover uma cultura organizacional onde os funcionários se sintam seguros para relatar erros ou interações suspeitas sem medo de punição. Encorajar a mentalidade de "confie, mas verifique".
