# Tipos de Evidência em Análise Forense Digital

## Introdução

A Análise Forense Digital é a ciência de identificar, preservar, analisar e apresentar evidências digitais de forma que sejam legalmente admissíveis. "Evidência digital" é qualquer informação de valor probatório que seja armazenada ou transmitida em formato digital. Diferente da evidência física, a evidência digital é extremamente frágil; ela pode ser alterada, danificada ou destruída com um simples clique ou ao se desligar um computador.

Por essa razão, um dos princípios mais importantes da forense é a **Ordem da Volatilidade**, que dita a sequência em que as evidências devem ser coletadas. O objetivo é capturar os dados mais efêmeros primeiro, antes que sejam irremediavelmente perdidos, e só depois coletar os dados mais permanentes.

---

### 1. A Hierarquia da Volatilidade: A Ordem da Coleta

A evidência digital existe em um espectro de volatilidade. A coleta em uma investigação, especialmente em um sistema ligado ("análise ao vivo"), deve seguir esta ordem, do mais para o menos volátil:

1.  **Registradores e Cache da CPU:** A informação mais volátil de todas, que muda a cada ciclo do processador. É raramente coletada na prática, mas representa o topo da hierarquia.

2.  **Memória RAM (Conteúdo da Memória Principal):** **Extremamente volátil e de altíssima importância**. O conteúdo da RAM é perdido assim que o sistema é desligado. Uma "cópia" da memória (memory dump) pode conter uma riqueza de evidências sobre o estado atual do sistema, incluindo:
    * Processos em execução (incluindo malwares que rodam apenas na memória).
    * Conexões de rede ativas.
    * Senhas e chaves de criptografia em texto claro.
    * Histórico de comandos digitados.
    * Conteúdo de arquivos e mensagens que foram abertos.

3.  **Dados de Rede e Processos do Sistema:** Informações sobre o estado da rede (`netstat`), processos ativos (`ps`), usuários logados e outras tabelas do sistema operacional. Estes dados mudam constantemente, mas de forma menos frenética que a RAM.

4.  **Dados em Dispositivos de Armazenamento:** A evidência "clássica". Inclui tudo o que está armazenado em discos rígidos (HDDs), unidades de estado sólido (SSDs) e pen drives. Por ser **persistente**, sobrevive a um desligamento do sistema.

5.  **Backups e Arquivos Remotos:** A forma mais estável e duradoura de evidência, geralmente armazenada em fitas, discos externos ou na nuvem.

A regra de ouro da resposta a incidentes deriva disso: **nunca desligue um sistema comprometido impulsivamente**, pois isso destruirá toda a evidência volátil contida na memória RAM.

---

### 2. Tipos de Evidência por Natureza: O que Procurar

Independentemente de onde a evidência é encontrada (na RAM ou no disco), ela pode ser classificada por sua natureza.

#### **Evidências do Sistema de Arquivos**
* **Arquivos Ativos:** Documentos, planilhas, imagens, e-mails, executáveis e logs criados pelo sistema ou pelo usuário.
* **Arquivos Deletados e Espaço Não Alocado:** Quando um arquivo é "deletado", geralmente apenas o ponteiro para ele é removido. Os dados brutos permanecem no disco até serem sobrescritos. Ferramentas forenses podem "esculpir" (carve) o espaço não alocado do disco para recuperar esses arquivos.
* **Metadados de Arquivos (MAC Times):** Todo arquivo possui carimbos de data/hora que são cruciais para a construção de uma linha do tempo: **M**odified (modificado), **A**ccessed (acessado) e **C**reated (criado).

#### **Evidências do Sistema Operacional**
* **Logs do Sistema:** A principal fonte de registro de atividades. No Windows, são os Logs de Eventos. No Linux, os arquivos em `/var/log` ou o `journalctl`.
* **Registro do Windows:** Um banco de dados hierárquico que armazena uma vasta quantidade de informações sobre configurações, softwares instalados, dispositivos USB que foram conectados ao sistema, senhas de Wi-Fi, e atividade do usuário.
* **Artefatos de Execução:** Áreas do sistema operacional que registram quais programas foram executados, quando e com que frequência (ex: Prefetch e ShimCache no Windows).

#### **Evidências da Rede**
* **Capturas de Pacotes (PCAPs):** Se um sniffer de rede estava ativo, as capturas contêm o tráfego de rede bruto, a "conversa" exata entre os sistemas.
* **Logs de Dispositivos:** Logs de firewalls, proxies, roteadores e servidores DNS fornecem um registro de todas as conexões que atravessaram a rede.

---

### 3. Os Princípios da Evidência Forense

Para que a evidência digital seja válida (especialmente em um contexto legal), ela deve aderir a princípios rigorosos.

* **Admissibilidade:** A evidência deve ser coletada de uma forma que seja legalmente aceitável.
* **Integridade e Cadeia de Custódia:** Este é o princípio mais importante.
    * **Hashing:** No momento da coleta, uma "impressão digital" criptográfica (um hash SHA256) da evidência original (ex: uma imagem de disco) é criada. Qualquer análise futura deve ser feita em uma cópia, e deve-se provar que o hash da cópia permanece idêntico ao original, garantindo que a evidência não foi adulterada.
    * **Cadeia de Custódia:** É a documentação cronológica e meticulosa que registra cada pessoa que manuseou a evidência, quando, onde e para qual finalidade. Isso garante a integridade do processo desde a coleta até a apresentação em tribunal.

### Conclusão

A análise forense digital lida com uma gama diversificada de evidências, desde os dados efêmeros da memória RAM até os arquivos persistentes em um disco rígido. O sucesso de uma investigação depende da capacidade do analista de compreender a natureza volátil dessas evidências, seguir um processo de coleta metodológico e manter uma cadeia de custódia rigorosa. Ao tratar cada peça de informação digital com o mesmo cuidado de uma evidência física, o analista forense pode reconstruir os eventos de um incidente de segurança com precisão e integridade.