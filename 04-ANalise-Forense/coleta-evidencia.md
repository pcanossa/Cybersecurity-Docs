# Coleta de Evidências Digitais Segundo a RFC 3227

## Introdução

A resposta a um incidente de segurança e a análise forense digital são disciplinas que exigem um rigor metodológico extremo. Qualquer ação mal planejada pode alterar ou destruir evidências cruciais, comprometendo permanentemente uma investigação. Para padronizar as melhores práticas nesse processo delicado, a Internet Engineering Task Force (IETF) publicou a **RFC 3227, "Guidelines for Evidence Collection and Archiving"** (Diretrizes para Coleta e Arquivamento de Evidências).

Este documento, embora não seja um padrão de internet, é considerado uma referência fundamental na comunidade de segurança. Ele estabelece um framework lógico para a coleta de evidências digitais, centrado em um princípio vital: a **Ordem da Volatilidade**.

---

### 1. O Princípio Fundamental: A Ordem da Volatilidade

O conceito mais importante da RFC 3227 é a Ordem da Volatilidade. Ele dita que, ao coletar evidências de um sistema computacional ativo ("análise ao vivo"), o analista deve sempre começar pelos dados mais voláteis (os que se perdem mais facilmente) e terminar com os dados mais persistentes.

A lógica é simples: você sempre pode extrair os dados de um disco rígido mais tarde, mas o conteúdo da memória RAM desaparece para sempre no momento em que o computador é desligado. A hierarquia de coleta, do mais para o menos volátil, é a seguinte:

1.  **Registradores e Caches da CPU:** Contêm os dados que estão sendo processados naquele exato instante. São extremamente voláteis e mudam a cada ciclo de clock.
2.  **Tabelas do Sistema e Caches Internos:** Inclui a tabela de processos, o cache ARP, a tabela de roteamento. Essas informações residem na RAM e refletem o estado atual do sistema operacional e da rede.
3.  **Memória Principal (RAM):** A fonte de evidência volátil mais valiosa. Uma cópia completa da RAM ("memory dump") pode conter:
    * Processos em execução (incluindo malwares sem arquivo).
    * Conexões de rede ativas.
    * Senhas e chaves de criptografia em texto claro.
    * Comandos executados recentemente.
4.  **Dados Temporários do Sistema de Arquivos:** Arquivos em diretórios como `/tmp` ou o arquivo de paginação (swap), que estão no disco, mas são frequentemente apagados durante um reboot.
5.  **Dados em Dispositivos de Armazenamento Persistente:** O conteúdo de discos rígidos (HDDs) e SSDs. É aqui que residem os arquivos do sistema, logs, e dados do usuário.
6.  **Dados Remotos e Arquivos de Backup:** Logs em um servidor Syslog central, backups em fita ou na nuvem. São os dados mais estáveis e menos voláteis.

---

### 2. Diretrizes Práticas da RFC 3227 para a Coleta

Além da ordem de coleta, a RFC estabelece outras diretrizes cruciais para garantir a integridade da evidência.

* **Minimizar as Alterações no Sistema:** O analista deve interagir o mínimo possível com o sistema comprometido para não alterar seu estado. Isso significa não executar programas do disco local. Em vez disso, deve-se usar um **toolkit forense confiável**, contendo versões estáticas e pré-compiladas das ferramentas de coleta, a partir de uma mídia externa de leitura-apenas (como um pen drive preparado).

* **Documentar Meticulosamente (Cadeia de Custódia):** Cada passo do processo de coleta deve ser rigorosamente documentado: a data e a hora, os comandos executados, a saída de cada comando, as pessoas presentes, etc. Essa documentação forma a **Cadeia de Custódia**, um registro cronológico que é essencial para provar a integridade da evidência em um contexto legal.

* **Trabalhar em Cópias (Imagens Forenses):** A análise nunca deve ser realizada diretamente na evidência original. A primeira etapa após a coleta de dados voláteis é criar uma **imagem forense** — uma cópia bit-a-bit do disco de armazenamento. Para garantir a integridade, um **hash criptográfico (SHA256)** é calculado tanto para o disco original quanto para a imagem. Os valores devem ser idênticos. Toda a análise subsequente é feita em uma cópia da imagem, preservando o original intacto.

* **Registrar o Tempo com Precisão:** A RFC enfatiza a importância de registrar a hora de cada ação e de sincronizar o relógio do sistema de análise com uma fonte de tempo confiável (usando **NTP**). É recomendado registrar os timestamps em formato Coordinated Universal Time (UTC) para evitar ambiguidades de fuso horário.

---

### 3. Um Fluxo de Trabalho Baseado na RFC 3227

Um processo de resposta a incidentes que segue as diretrizes da RFC 3227 poderia se parecer com isto:

1.  **Preparação:** Chegar ao local com um toolkit forense em mídia externa e equipamento para a criação de imagens de disco.
2.  **Documentação Inicial:** Registrar a cena, o estado do computador (ligado/desligado) e a hora.
3.  **Coleta de Dados Voláteis (se o sistema estiver ligado):**
    * Conectar o toolkit forense.
    * Executar comandos para capturar o estado da rede, processos, etc., redirecionando a saída para um disco externo.
    * Realizar um *dump* completo da memória RAM para um disco externo.
4.  **Coleta de Dados Persistentes:**
    * Conectar um bloqueador de escrita (*write blocker*) ao disco do sistema para impedir qualquer alteração.
    * Criar uma imagem forense bit-a-bit do disco.
    * Calcular e registrar os hashes do disco original e da imagem.
5.  **Desligamento e Armazenamento:** Desligar o sistema e armazenar a evidência original de forma segura, documentando na Cadeia de Custódia.
6.  **Análise:** Realizar toda a análise em uma cópia da imagem forense, em um ambiente de laboratório seguro.

### Conclusão

A IETF RFC 3227 fornece um framework lógico e essencial para a disciplina de forense digital. Seu princípio central, a **Ordem da Volatilidade**, é a regra de ouro que guia a coleta de evidências em sistemas ativos, garantindo que as informações mais frágeis e, muitas vezes, mais incriminadoras, sejam preservadas. Ao aderir a essas diretrizes, um analista não apenas maximiza a quantidade de evidências recuperadas, mas também garante a integridade e a admissibilidade de suas descobertas, formando a base de uma investigação técnica e legalmente sólida.