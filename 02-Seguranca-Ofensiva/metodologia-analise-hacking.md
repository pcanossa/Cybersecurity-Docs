# A Metodologia de um Teste de Intrusão

**Data de Publicação:** 28 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução

O Hacking Ético, ou Teste de Intrusão (Penetration Test), é a prática de simular um ciberataque contra os próprios sistemas de uma organização, com autorização prévia, para descobrir e corrigir vulnerabilidades antes que um ator malicioso possa explorá-las. Longe de ser um processo aleatório, um teste de intrusão profissional segue uma metodologia estruturada e disciplinada. As "5 Fases do Hacking" representam o padrão da indústria para essa metodologia, fornecendo um roteiro que vai desde a coleta inicial de informações até a remoção de evidências, espelhando exatamente as ações de um adversário real. Este artigo detalha cada uma dessas fases, contextualizando onde os ataques que já discutimos se encaixam neste processo.

---

### Fase 1: Reconhecimento (Reconnaissance)

Esta é a fase de coleta de informações. O objetivo é aprender o máximo possível sobre o alvo para identificar potenciais vetores de ataque, sem ainda lançar um ataque direto.

* **Objetivo:** Traçar o perfil da organização, sua infraestrutura, pessoal e tecnologias.
* **Atividades:**
    * **Reconhecimento Passivo (OSINT):** Coletar informações de fontes públicas sem interagir diretamente com o alvo. Isso inclui pesquisar no Google, analisar o site da empresa, perfis de funcionários no LinkedIn, registros de DNS públicos e vazamentos de dados.
    * **Reconhecimento Ativo:** Interagir diretamente com a infraestrutura do alvo para obter respostas. É aqui que entram os ataques que vimos no artigo sobre **Mitigação de Ataques de Reconhecimento**, como varreduras de ping (`Ping Sweeps`) para descobrir hosts ativos.
* **Resultado:** Uma lista de alvos potenciais, como endereços IP, nomes de domínio, endereços de e-mail de funcionários e informações sobre a tecnologia utilizada pela empresa.

---

### Fase 2: Varredura e Sondagem (Scanning)

Com a lista de alvos da fase anterior, o atacante agora procura por portas abertas e vulnerabilidades específicas que possam ser exploradas.

* **Objetivo:** Identificar pontos de entrada exploráveis.
* **Atividades:**
    * **Varredura de Portas:** Usar ferramentas como o Nmap para descobrir quais portas TCP e UDP estão abertas em um host, revelando os serviços em execução (ex: um servidor web na porta 443, um servidor de e-mail na porta 25).
    * **Varredura de Vulnerabilidades:** Usar scanners automatizados (como Nessus ou OpenVAS) para cruzar os serviços encontrados com um banco de dados de vulnerabilidades conhecidas (CVEs).
* **Resultado:** Um mapa detalhado dos sistemas do alvo, listando os serviços ativos e as vulnerabilidades específicas associadas a eles. É nesta fase que as **vulnerabilidades de TCP, UDP e IP** que discutimos são identificadas.

---

### Fase 3: Obtenção de Acesso (Gaining Access)

Esta é a fase onde o ataque realmente acontece. O hacker usa as informações das fases 1 e 2 para explorar uma vulnerabilidade e obter seu primeiro acesso ao sistema.

* **Objetivo:** Conseguir um "pé na porta", mesmo que seja com privilégios limitados.
* **Atividades:** A exploração pode ocorrer em várias camadas:
    * **Nível de Rede:** Explorar uma vulnerabilidade em um serviço de rede sem patch.
    * **Nível de Aplicação:** Executar um ataque de **Injeção de SQL** para contornar uma tela de login ou um **Cross-Site Scripting (XSS)** para roubar o cookie de sessão de um administrador.
    * **Nível Humano:** Enviar um e-mail de **phishing** para um funcionário para que ele entregue suas credenciais.
* **Resultado:** O atacante obtém acesso a um sistema, seja como um usuário de baixo privilégio, um usuário de aplicação ou, no melhor dos casos para ele, como administrador. Esta fase é a aplicação prática de quase todos os artigos sobre **ataques de acesso, e-mail, e aplicações web** que analisamos.

---

### Fase 4: Manutenção de Acesso (Maintaining Access)

Uma vez dentro, o objetivo do atacante é garantir que ele possa retornar ao sistema comprometido no futuro, mesmo que o sistema seja reiniciado ou a vulnerabilidade original seja corrigida.

* **Objetivo:** Estabelecer uma presença persistente e de longo prazo.
* **Atividades:**
    * **Instalação de Backdoors e Trojans:** Deixar um "caminho" aberto para acesso futuro.
    * **Criação de Contas:** Adicionar novas contas de usuário, muitas vezes com privilégios de administrador.
    * **Escalada de Privilégios:** Usar exploits locais para transformar um acesso de usuário comum em acesso de administrador (root/system).
    * **Estabelecimento de Canais Secretos (C2):** Utilizar técnicas como o **Tunelamento de DNS** para criar um canal de Comando e Controle que não seja detectado por firewalls.
* **Resultado:** O sistema se torna um "zumbi" ou "bot", que pode ser controlado remotamente pelo atacante. Como vimos no diagrama da botnet, esta fase é crucial para manter o controle dos ativos comprometidos.

---

### Fase 5: Apagando os Rastros (Covering Tracks)

Para evitar a detecção e manter o acesso persistente, o atacante tentará remover todas as evidências de sua presença e atividades.

* **Objetivo:** Evitar a detecção por administradores de sistema e analistas de segurança.
* **Atividades:**
    * **Limpeza de Logs:** Alterar, modificar ou apagar entradas nos logs de sistema (`/var/log/` no Linux, Logs de Eventos do Windows) que registram suas ações, como logins e execução de comandos.
    * **Uso de Rootkits:** Instalar malwares que se integram ao núcleo (kernel) do sistema operacional para esconder arquivos, processos e conexões de rede da vista do administrador.
    * **Uso de Esteganografia:** Ocultar dados roubados dentro de arquivos de imagem ou áudio para exfiltrá-los sem levantar suspeitas.
* **Resultado:** A investigação forense do incidente se torna muito mais difícil. Esta fase é uma batalha direta contra as técnicas que vimos no artigo de **Análise de Logs**. A centralização de logs em um servidor SIEM (para onde o atacante não tem acesso) é a principal contramedida.

### O Relatório

Nesta etapa, o profissional documenta detalhadamente todas as vulnerabilidades encontradas, as técnicas utilizadas para explorá-las e, o mais importante, fornece recomendações claras e acionáveis para que a organização possa corrigir as falhas e fortalecer sua postura de segurança.