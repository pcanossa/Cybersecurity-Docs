# Análise Técnica do Grupo de Ameaça: Scattered Spider (AA23-320A)

**Data de Publicação:** 14 de agosto de 2025  
**Nível de Ameaça:** Crítico 
**Autor:** Patrícia Canossa (com base em relatório do CISA e FBI)

---

### 1. Resumo Executivo

Este documento fornece uma análise técnica do grupo de ameaças rastreado como `Scattered Spider` (também conhecido como **Octo Spider**, **Starfraud**, **UNC3944**). O grupo é composto por atores de língua inglesa, financeiramente motivados, que demonstram alta proficiência em *engenharia social* e abuso de ferramentas legítimas para obter acesso inicial, mover-se lateralmente e exfiltrar dados para fins de extorsão. Recentemente, o grupo escalou suas operações para incluir a implantação de ransomware, notavelmente o **BlackCat/ALPHV**. O alerta da CISA detalha seus TTPs para ajudar as organizações a fortalecer suas defesas contra este ator prolífico e adaptável.

### 2. Perfil do Grupo e Setores Alvo

* **Identidade e Motivação:** Grupo de língua inglesa, composto por múltiplos membros, com motivação puramente financeira.  
* **Expertise Principal:** Engenharia social, abuso de identidade e exploração de configurações de nuvem.  
* **Setores Alvo:** Demonstram preferência por grandes corporações e provedores de serviços de TI, incluindo:  
  * Telecomunicações  
  * Terceirização de Processos de Negócios (BPO)  
  * Mídia e Entretenimento  
  * Setor Financeiro e Seguros  
  * Tecnologia e Varejo

O objetivo é infiltrar-se em organizações que possuem grandes volumes de dados de clientes ou que podem servir como um ponto de entrada para outras vítimas (no caso de provedores de serviços).

### 3. Cadeia de Ataque e TTPs (Táticas, Técnicas e Procedimentos)

O Scattered Spider emprega uma cadeia de ataque metódica, combinando engenharia social com abuso de ferramentas legítimas (**Living-off-the-Land - LotL**).

**Fase 1: Acesso Inicial**

* **Engenharia Social (T1566):** Utilizam Vishing e Phishing para se passar por funcionários de TI, visando o *help desk* ou diretamente os funcionários.  
* **Ataques de Fadiga de MFA (T1621):** Bombardeiam os usuários com notificações *push* de Autenticação Multifator até que a vítima aprove uma por engano.  
* **Troca de SIM (SIM Swapping):** Comprometimento do número de telefone da vítima para interceptar códigos MFA enviados por SMS.  
* **Abuso de Ferramentas de Acesso Remoto:** Convencem as vítimas a instalar softwares legítimos de RMM (Remote Monitoring and Management) como `TeamViewer`, `ScreenConnect` e `AnyDesk`, concedendo-lhes acesso direto à máquina da vítima.

**Fase 2: Execução e Persistência**

* **Criação de Contas Locais (T1136.001):** Criam contas de usuário no sistema comprometido para garantir acesso persistente.  
* **Abuso de Softwares de RMM Legítimos (T1219):** Instalam e configuram ferramentas como `Fleetdeck.io`, `ConnectWise ScreenConnect` e `AnyDesk` como um serviço, garantindo que o acesso seja restabelecido após reinicializações.  
* **Agendamento de Tarefas (T1053.005):** Criam tarefas agendadas para executar seus scripts ou restabelecer conexões.

**Fase 3: Escalação de Privilégios e Acesso a Credenciais**

* **Dumping de LSASS (T1003.001):** Utilizam ferramentas como `Mimikatz` e `procdump.exe` para extrair credenciais da memória do processo `LSASS`.  
* **Kerberoasting (T1558.003):** Exploram o protocolo `Kerberos` para obter hashes de senhas de contas de serviço, que podem ser quebrados offline.  
* **Extração de Segredos do Navegador:** Utilizam scripts para roubar senhas e cookies salvos em navegadores.

**Fase 4: Evasão de Defesa**

* **Desativação de Ferramentas de Segurança (T1562.001):** Utilizam seus privilégios elevados para desinstalar ou desabilitar softwares de **EDR (Endpoint Detection and Response)** e **antivírus**.  
* **Limpeza de Logs (T1070):** Apagam logs de eventos do *Windows* para ocultar suas atividades.  
* **Uso de Ferramentas de Dual-Use:** Empregam ferramentas legítimas como `ngrok` e socat para criar túneis criptografados, dificultando a inspeção do tráfego de rede.


**Fase 5: Descoberta e Movimentação Lateral**

* **Descoberta de Rede:** Utilizam comandos nativos como `ipconfig`, `netstat`, `nltest` e `dsquery` para mapear a rede e a topologia do `Active Directory`.  
* **Ferramentas de Scanner:** Empregam scanners como `nmap` e `AdFind` para um reconhecimento mais detalhado.  
* **Protocolos de Acesso Remoto:** Abusam extensivamente de **`RDP` (T1021.001)** e **`SSH` (T1021.004)** para se mover entre os sistemas na rede.

**Fase 6: Coleta, Exfiltração e Impacto**

* **Coleta de Dados:** Focam em dados de ambientes de nuvem (**Azure**, **AWS**, **GCP**) e de plataformas como **Okta**, **vCenter** e **Salesforce**.  
* **Exfiltração via Ferramentas de Nuvem (T1567.002):** Utilizam ferramentas como `Rclone` e o `MEGAsync client` para transferir grandes volumes de dados para serviços de armazenamento em nuvem sob seu controle.  
* **Impacto Final - Ransomware (T1486):** Após a exfiltração, eles criptografam os sistemas da vítima usando o ransomware **BlackCat/ALPHV**, completando a dupla extorsão (pagamento para não vazar os dados e para obter a chave de descriptografia).

### 4. Ferramentas e Infraestrutura Notáveis

O grupo utiliza uma mistura de ferramentas de código aberto, softwares comerciais e comandos nativos:

| Categoria | Ferramentas Utilizadas |
| :---- | :---- |
| **Acesso Remoto** | AnyDesk, TeamViewer, ScreenConnect, Fleetdeck.io, Splashtop, Atera |
| **Acesso a Credenciais** | Mimikatz, LaZagne, Procdump, Trufflehog |
| **Túneis e Rede** | ngrok, socat, PuTTY/Plink, Nmap, AdFind |
| **Exfiltração** | Rclone, MEGAsync |
| **Ransomware** | BlackCat / ALPHV |

### 5. Mitigação e Recomendações da CISA

A CISA e o FBI recomendam uma abordagem de defesa em profundidade:

1. **Gestão de Identidade e Acesso (IAM):**  
   * Implementar **MFA resistente a phishing** (*FIDO2/WebAuthn*) para todos os serviços, especialmente para contas de administrador.  
   * Limitar o número de tentativas de MFA e alertar sobre atividades de *spamming* de MFA.  
   * Aplicar o **princípio do menor privilégio** e revisar regularmente as permissões de acesso.  
2. **Segurança de Rede e Endpoint:**  
   * Revisar e restringir o uso de ferramentas de RMM. Bloquear a instalação de softwares não autorizados.  
   * Segmentar a rede para impedir a movimentação lateral.  
   * Garantir que as ferramentas de **EDR/antivírus** tenham proteção contra adulteração (*tamper protection*) ativada.  
   * Monitorar o tráfego de rede em busca de túneis suspeitos (ex: `ngrok`) e conexões para serviços de nuvem desconhecidos.  
3. **Processos e Treinamento:**  
   * Fortalecer os processos de verificação de identidade no *help desk* para solicitações de redefinição de senha/MFA.  
   * Treinar os funcionários para reconhecer táticas de engenharia social, especialmente Vishing e fadiga de MFA.  
   * Criar um procedimento claro para que os funcionários relatem imediatamente qualquer tentativa de engenharia social.  
4. **Monitoramento e Resposta:**  
   * Habilitar e centralizar logs de todos os sistemas críticos (endpoints, servidores, nuvem).  
   * Monitorar a criação de contas de usuário locais e o uso de comandos suspeitos de `PowerShell` e `wmic`.  
   * Desenvolver e testar um plano de resposta a incidentes que inclua cenários de ransomware e extorsão de dados.