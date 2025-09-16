# Guia Coleta Básica de Informações Pós-Incidente

## Introdução

Quando um incidente de segurança ocorre, a resposta rápida e metódica é crucial. Uma equipe de resposta a incidentes de segurança em computadores (CSIRT) é responsável por gerenciar essa resposta, e uma de suas primeiras e mais importantes tarefas é a coleta de informações do sistema comprometido.

Este processo é uma corrida contra o tempo, pois dados vitais que residem na memória RAM são voláteis e desaparecerão assim que o sistema for desligado. Este artigo detalha um procedimento prático para coletar informações críticas do sistema e revisar logs, garantindo que as evidências necessárias para a análise do incidente sejam preservadas.

---

### 1. Coleta de Informações Voláteis

A primeira fase da coleta foca nos dados que não sobreviveriam a uma reinicialização. A estratégia é criar um único arquivo de relatório (ex: `report.txt`) que consolida um "snapshot" do estado do sistema no momento da investigação. Este relatório pode então ser transferido para uma unidade USB, enviado por e-mail ou carregado para um servidor em nuvem para preservação antes que o sistema seja desativado.

O processo, executado com privilégios de superusuário (`root`), envolve os seguintes passos:

* **Início e Timestamp:** O relatório é iniciado com um cabeçalho e um carimbo de data/hora para marcar o início preciso da coleta.
    * `echo Relatórios dos investigadores > report.txt`
    * `date >> report.txt`

* **Coleta de Informações do Sistema:** O comando `uname -a` é usado para acrescentar ao relatório todas as informações do sistema, como a versão do kernel e a arquitetura, identificando a plataforma exata que foi comprometida.

* **Coleta de Configuração de Rede:** O comando `ifconfig -a` é executado para acrescentar todas as informações das interfaces de rede ao relatório, documentando como o sistema estava configurado na rede.

* **Coleta de Estatísticas de Rede:** Utiliza-se o comando `netstat -ano` para coletar dados sobre todos os soquetes (`-a`), exibir endereços IP em vez de nomes de domínio (`-n`), e incluir informações de timers de rede (`-o`). Essa etapa é crucial para identificar conexões de rede ativas que poderiam estar associadas ao incidente.

* **Coleta de Processos em Execução:** O comando `ps axu` relata um snapshot dos processos atuais. As opções `axu` listam todos os processos em execução no sistema em um formato orientado ao usuário, permitindo a identificação de qualquer processo malicioso ou não autorizado.

* **Coleta da Tabela de Roteamento:** O comando `route -n` é usado para listar a tabela de roteamento do sistema em formato numérico. Isso ajuda a entender como o tráfego de rede estava sendo direcionado pelo host comprometido.

* **Timestamp Final:** Um carimbo de data/hora final é adicionado com o comando `date` para concluir o relatório, delimitando claramente o período da coleta de dados voláteis.

---

### 2. Análise de Logs Persistentes

Além dos dados voláteis armazenados na RAM, o sistema mantém uma variedade de logs em disco que devem ser revisados após um incidente. Esses arquivos de log podem ser anexados ao `report.txt` ou armazenados separadamente. Os registros de particular interesse incluem:

* **`auth.log`:** Registra informações de autorização do sistema. Este log pode ser visualizado com o comando `cat /var/log/auth.log | less` para investigar atividades de login e uso de privilégios.
* **`btmp.log`:** Registra as tentativas de login com falha. O comando `last -f /var/log/btmp` pode ser usado para rapidamente identificar possíveis ataques de força bruta.
* **`wtmp.log`:** Registra quem está ou esteve logado no sistema. O comando `last -f /var/log/wtmp` mostra um histórico de logins bem-sucedidos, reboots do sistema e sessões de usuário.

### Conclusão

A coleta de informações imediatamente após um incidente é uma etapa crítica que exige precisão e velocidade. Seguindo um procedimento estruturado, como o detalhado acima, uma CSIRT pode garantir a preservação tanto dos dados voláteis (o estado momentâneo do sistema) quanto dos dados persistentes (os registros históricos de log). Essa coleta abrangente de evidências é o que permite uma análise forense eficaz, possibilitando que a equipe entenda a natureza do comprometimento, contenha a ameaça e desenvolva estratégias para prevenir futuros incidentes.