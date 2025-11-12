# Estrutura do Sistema de Arquivos Linux (FHS)

## Introdução

O Linux apresenta uma única árvore de diretórios unificada, que começa em um único ponto: a **raiz**, representada por uma barra (`/`). Ela é governada pelo **Filesystem Hierarchy Standard (FHS)**, um padrão que define os principais diretórios e seu conteúdo. O objetivo do FHS é garantir que, independentemente da distribuição Linux (Ubuntu, CentOS, Arch), um usuário ou um software possa prever onde encontrar os arquivos e recursos necessários. Um dos princípios filosóficos do UNIX/Linux é que **"tudo é um arquivo"**, e o FHS é o mapa que organiza todos esses "arquivos", desde programas e configurações até os próprios dispositivos de hardware.

---

### 1. A Raiz (`/`)

Todo e qualquer arquivo ou diretório no Linux está contido dentro do diretório raiz (`/`). É o topo da hierarquia, a partir do qual todos os outros diretórios se ramificam.

---

### 2. Os Diretórios Essenciais do Sistema

Este grupo de diretórios contém os arquivos cruciais para a inicialização (boot) e o funcionamento básico do sistema. Eles devem estar disponíveis mesmo que outras partes do sistema de arquivos (como o `/usr`) ainda não estejam montadas.

* **`/bin` (Binaries):** Contém os **binários executáveis essenciais** que estão disponíveis para todos os usuários do sistema, incluindo os comandos mais básicos como `ls`, `cp`, `mv`, `cat`, e o próprio shell (`bash`).

* **`/sbin` (System Binaries):** Contém os **binários de sistema essenciais**, comandos que são geralmente reservados para o superusuário (`root`) para tarefas de administração. Exemplos incluem `ifconfig` (configuração de rede), `fdisk` (particionamento de disco) e `reboot`.

* **`/etc` (Etcetera):** Este é o centro nevrálgico da **configuração** do sistema. Contém todos os arquivos de configuração para todo o sistema e para a maioria dos serviços. Arquivos como `passwd` (usuários), `fstab` (montagem de discos), `sshd_config` (configuração do SSH) residem aqui. É um dos diretórios mais importantes para um administrador de sistemas e analista de segurança.

* **`/lib` (Libraries):** Contém as **bibliotecas compartilhadas essenciais** (`.so` - shared objects) que são necessárias para os binários em `/bin` e `/sbin` funcionarem. São como os arquivos `.dll` no Windows.

* **`/boot`:** Contém os arquivos necessários para o processo de inicialização do sistema, incluindo o **kernel do Linux** e os arquivos do gerenciador de boot (como o GRUB).

---

### 3. Dados de Usuários e Aplicações

* **`/home`:** O diretório onde cada **usuário padrão** tem sua pasta pessoal. Por exemplo, o seu diretório pessoal seria `/home/(usuario)`. É aqui que são armazenados documentos, downloads, e arquivos de configuração específicos de um usuário.

* **`/root`:** O diretório "home" exclusivo do **superusuário (root)**.

* **`/var` (Variable):** Contém arquivos de **dados variáveis**, cujo conteúdo e tamanho mudam constantemente durante a operação do sistema. É um diretório crucial para monitoramento e análise.
    * **`/var/log`:** A localização padrão para todos os **arquivos de log** do sistema e de serviços. Para um analista de segurança, este é um dos diretórios mais importantes do sistema.
    * **`/var/spool`:** Contém filas (spools) de tarefas, como e-mails a serem enviados ou trabalhos de impressão.

---

### 4. A Hierarquia Secundária e Diretórios de Aplicações

* **`/usr` (Unix System Resources):** **Não confundir com "user"**. Este é um dos maiores diretórios e contém a maioria dos softwares, bibliotecas e dados que não são absolutamente essenciais para a inicialização do sistema. Ele espelha a estrutura da raiz, contendo seus próprios subdiretórios:
    * **`/usr/bin`:** Binários para usuários que não são essenciais para o boot. A grande maioria dos programas que você instala fica aqui.
    * **`/usr/sbin`:** Binários de administração de sistema não essenciais.
    * **`/usr/lib`:** Bibliotecas para os programas em `/usr/bin` e `/usr/sbin`.
    * **`/usr/share`:** Dados compartilhados que são independentes da arquitetura, como documentação (`/usr/share/doc`) e ícones.

* **`/opt` (Optional):** Usado para a instalação de softwares "opcionais" e de terceiros que não seguem a estrutura padrão do sistema. Softwares como o Google Chrome ou o Zoom frequentemente se instalam aqui.

* **`/tmp` (Temporary):** Contém arquivos temporários criados por usuários e aplicações. O conteúdo deste diretório é geralmente apagado a cada reinicialização do sistema.

* **`/mnt` (Mount) e `/media`:** Diretórios usados como ponto de montagem para sistemas de arquivos temporários, como pen drives (`/media`) ou partições de disco montadas manualmente (`/mnt`).

---

### 5. Os Sistemas de Arquivos Virtuais

Estes não são diretórios "reais" no disco, mas sim interfaces virtuais, geradas em tempo real pelo kernel, que expõem informações sobre o estado do sistema.

* **`/proc` (Processes):** Contém informações sobre os processos em execução e o estado do kernel. Cada processo em execução tem seu próprio diretório numerado aqui. Ferramentas como `ps` e `top` obtêm suas informações lendo os arquivos virtuais dentro do `/proc`.

* **`/sys` (System):** Expõe informações sobre os dispositivos de hardware e drivers do sistema.

---

### Tabela Resumo

| Diretório | Nome Completo | Função Principal |
| :--- | :--- | :--- |
| **`/`** | Root | O diretório raiz de toda a hierarquia. |
| **`/bin`** | Binaries | Comandos essenciais para todos os usuários. |
| **`/sbin`** | System Binaries | Comandos de administração do sistema. |
| **`/etc`** | Etcetera | Arquivos de configuração de todo o sistema. |
| **`/lib`** | Libraries | Bibliotecas essenciais para `/bin` e `/sbin`. |
| **`/boot`** | Boot | Arquivos do processo de inicialização (kernel). |
| **`/home`** | Home | Diretórios pessoais dos usuários. |
| **`/root`** | Root | Diretório pessoal do superusuário. |
| **`/var`** | Variable | Arquivos variáveis (logs, spools, etc.). |
| **`/usr`** | Unix System Resources | Programas, bibliotecas e dados não essenciais para o boot. |
| **`/opt`** | Optional | Software de terceiros. |
| **`/tmp`** | Temporary | Arquivos temporários. |
| **`/mnt` / `/media`**| Mount / Media | Pontos de montagem para dispositivos externos. |
| **`/proc` / `/sys`**| Processes / System | Sistemas de arquivos virtuais do kernel. |

---

### Por que a Estrutura é Crucial para a Cibersegurança?

* **Análise Forense:** Saber onde procurar é metade da batalha. Logs estão em `/var/log`, configurações em `/etc`, binários do sistema em `/bin` e `/sbin`.
* **Detecção de Persistência:** Um atacante frequentemente tentará manter o acesso colocando scripts ou binários maliciosos em locais como `/tmp` ou no diretório home do usuário.
* **Endurecimento (Hardening):** A segurança de um sistema Linux envolve a aplicação de permissões rigorosas a esses diretórios, garantindo, por exemplo, que usuários normais não possam modificar arquivos em `/sbin` ou `/etc`.
* **Monitoramento de Integridade:** Ferramentas de segurança monitoram diretórios críticos como `/bin`, `/sbin` e `/etc` em busca de qualquer alteração não autorizada, o que pode indicar um comprometimento.

### Conclusão

A Estrutura do Sistema de Arquivos Linux, padronizada pelo FHS, é uma organização lógica e previsível que traz ordem ao ecossistema. 