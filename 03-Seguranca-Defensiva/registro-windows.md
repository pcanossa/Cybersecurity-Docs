# Análise do Registro do Windows para Investigações de Cibersegurança

## Resumo Executivo
O **Registro do Windows** é o banco de dados de configuração central do sistema operacional, operando como a "caixa preta" que armazena todas as configurações de hardware, software, políticas e comportamento do sistema. Para profissionais de cibersegurança, especialmente em áreas como **Resposta a Incidentes e Forense Digital (DFIR)**, **Centros de Operações de Segurança (SOC)** e **Caça a Ameaças (Threat Hunting)**, o Registro é uma fonte essencial e indispensável de evidências.

A análise de chaves específicas revela rastros de atividades maliciosas, incluindo mecanismos de persistência, evasão de defesas, backdoors, execução de scripts não autorizados e o histórico de atividades do usuário que precederam um incidente. A manipulação dessas chaves permite que malwares operem livremente, mantenham o acesso a sistemas comprometidos e exfiltrem dados de forma discreta. Este documento detalha oito áreas críticas de investigação dentro do Registro, fornecendo um roteiro para identificar e compreender atividades adversárias.

---

## Pontos Críticos de Análise no Registro do Windows

A seguir, são detalhadas as chaves e áreas do Registro que servem como indicadores cruciais durante uma investigação de segurança.

### 1. Persistência via Chaves `Run` e `RunOnce`
Essas chaves são um dos métodos mais comuns para garantir que um programa seja executado automaticamente na inicialização do sistema.

| Chave de Registro | Descrição do Risco |
| :--- | :--- |
| `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` | Programas que iniciam com o logon do **usuário atual**. |
| `HKLM\Software\Microsoft\Windows\CurrentVersion\Run` | Programas que iniciam com o sistema para **todos os usuários**. |

* **Uso Malicioso:** Atacantes adicionam entradas nessas chaves para executar seus payloads a cada logon, garantindo a persistência do malware no sistema.
* **Indicadores de Comprometimento:** A presença de executáveis (`.exe`), scripts de lote (`.bat`) ou scripts VBS (`.vbs`) desconhecidos é um forte indicador de comprometimento.

### 2. Configuração Insegura do PowerShell
A política de execução do PowerShell determina o nível de permissão para a execução de scripts, sendo um alvo comum para atacantes.

* **Chave de Registro:** `HKCU\Software\Microsoft\PowerShell\1\ShellIds\Microsoft.PowerShell\ExecutionPolicy`
* **Uso Malicioso:** Atacantes alteram essa política para permitir a execução irrestrita de scripts maliciosos.
* **Indicadores de Comprometimento:** Valores como `Unrestricted`, `Bypass` ou `Undefined` indicam uma política de execução permissiva que pode ser abusada.

### 3. Desativação do Controle de Conta de Usuário (UAC)
O UAC é uma camada de segurança que exige confirmação para ações que requerem privilégios administrativos. Sua desativação remove essa proteção.

* **Chave de Registro:** `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\EnableLUA`
* **Uso Malicioso:** Malwares frequentemente desativam o UAC para poderem executar ações privilegiadas livremente, sem alertar o usuário através de prompts administrativos.
* **Indicadores de Comprometimento:** Um valor de `0` na chave `EnableLUA` significa que o UAC está **desativado**, expondo o sistema a operações maliciosas sem restrições.

### 4. Forçamento de Proxy como Técnica de Evasão
A manipulação das configurações de proxy do sistema permite que um atacante intercepte e redirecione o tráfego de rede.

* **Chave de Registro:** `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\ProxyEnable`
* **Uso Malicioso:** Através da alteração do proxy, um atacante pode redirecionar o tráfego para servidores maliciosos, interceptar dados, estabelecer comunicação com servidores de Comando e Controle (C2) e exfiltrar informações de forma mais discreta.
* **Indicadores de Comprometimento:** Qualquer alteração não planejada ou não autorizada nas configurações de proxy é um alerta significativo.

### 5. Chaves "Genéricas" Criadas por Malware
Malwares frequentemente criam suas próprias chaves de registro para armazenar configurações, caminhos de arquivos e outros dados necessários para manter o ataque ativo.

* **Locais Comuns:** `HKCU\Software\` e `HKLM\Software\`
* **Uso Malicioso:** São criadas pastas com nomes que parecem inofensivos ou legítimos para não levantar suspeitas.
* **Indicadores de Comprometimento:** Fique atento a nomes de chaves suspeitos como `systemupdate`, `winhelper`, `svchost123` ou `updater32`.

### 6. Habilitação Indevida do RDP (Remote Desktop Protocol)
O RDP é uma porta de acesso remoto legítima, mas quando habilitado sem justificativa, torna-se um backdoor poderoso para atacantes.

* **Chave de Registro:** `HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\fDenyTSConnections`
* **Uso Malicioso:** Após o comprometimento inicial, atacantes habilitam o RDP para garantir acesso remoto persistente ao sistema.
* **Indicadores de Comprometimento:** * Um valor de `0` nesta chave indica que o RDP está **habilitado**. Se não houver uma justificativa administrativa para isso, é um sinal de alerta de um possível backdoor.
    * Um valor de `1` indica que o RDP está **bloqueado**.

### 7. Histórico de Acesso a Arquivos (MRU - Most Recently Used)
Esta área do registro armazena um histórico dos arquivos que o usuário acessou recentemente, fornecendo um rastro valioso de suas atividades.

* **Chave de Registro:** `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`
* **Uso em Investigação:** A análise dessa chave ajuda a identificar qual arquivo pode ter iniciado um incidente (ex: um documento malicioso), compreender o comportamento do usuário antes da infecção e encontrar evidências de engenharia social ou manipulação de documentos.

### 8. Persistência Silenciosa via `StartupApproved`
Esta chave registra programas que foram aprovados para iniciar com o sistema, incluindo aqueles que não aparecem nas chaves `Run` mais comuns, tornando-se um método de persistência mais discreto.

* **Chave de Registro:** `HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\StartupApproved\Run`
* **Uso Malicioso:** Por ser uma localização menos óbvia e menos monitorada, é frequentemente utilizada por malwares para garantir sua inicialização discreta a cada logon.

---

## Conclusão

A análise aprofundada do Registro do Windows é fundamental para descobrir um amplo espectro de táticas, técnicas e procedimentos adversários. As investigações podem revelar um conjunto diversificado de evidências, incluindo:

* **Persistência:** Mecanismos usados por malware para sobreviver a reinicializações.
* **Evasão:** Técnicas para contornar defesas, como a manipulação de proxies.
* **Backdoors:** Portas de acesso remoto abertas para garantir o retorno do atacante.
* **Ajustes Suspeitos:** Alterações em políticas de segurança, como a desativação do UAC.
* **Histórico Pré-Incidente:** Rastro de arquivos abertos que podem ter sido o vetor de infecção.
* **Comportamento Anômalo:** Criação de chaves de registro com nomes genéricos e suspeitos.
* **Rastro de Malware:** Configurações e dados armazenados pelo próprio malware para sua operação.