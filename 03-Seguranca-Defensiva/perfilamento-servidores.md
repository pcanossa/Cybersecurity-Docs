# Perfilamento de Servidores

## Introdução

Um servidor em uma rede nunca é uma entidade estática. Ele executa processos, atende a requisições, e seu estado muda constantemente. Em meio a essa atividade incessante, como um analista de segurança ou administrador de sistemas pode diferenciar o comportamento "normal" de uma anomalia que indica um problema de performance ou, pior, um comprometimento de segurança?

A resposta está no **perfilamento de servidores**, também conhecido como **criação de linha de base (baselining)**. Este é o processo de documentar e entender o estado e o comportamento normais e esperados de um servidor quando ele está operando em condições ideais. Essa "fotografia" do estado saudável serve como um ponto de referência crucial. Qualquer desvio significativo dessa linha de base se torna um sinal de alerta, permitindo uma detecção e resposta muito mais rápidas.

---

### 1. Por que o Perfilamento é Essencial?

Criar e manter uma linha de base de um servidor não é apenas uma boa prática; é um pilar para diversas funções críticas de TI e segurança.

* **Detecção de Anomalias de Segurança:** Esta é a aplicação mais crítica. Sem saber como é o "normal", é impossível identificar o "anormal". Um novo serviço escutando em uma porta de rede, um processo desconhecido consumindo CPU, ou uma conta de usuário que nunca fez login acessando o sistema, são todos desvios da linha de base que podem indicar a presença de um malware ou de um invasor.

* **Análise de Performance e Troubleshooting:** Uma linha de base de métricas de desempenho (CPU, memória, I/O de disco) permite que os administradores identifiquem gargalos, entendam o impacto de novas aplicações e diagnostiquem problemas de lentidão de forma muito mais eficaz.

* **Planejamento de Capacidade (Capacity Planning):** Ao monitorar as tendências de uso de recursos em relação à linha de base, as equipes de TI podem prever com precisão quando será necessário adicionar mais memória, CPU ou espaço em disco, evitando falhas por esgotamento de recursos.

* **Auditoria e Conformidade (Compliance):** Um perfil bem documentado serve como evidência de uma configuração de sistema conhecida e segura (um "golden image"), o que é frequentemente um requisito para auditorias de segurança e conformidade com regulamentações como a LGPD ou o PCI-DSS.

---

### 2. O "Check-up" do Servidor: O que Coletar?

Um perfil de servidor abrangente deve documentar vários aspectos do sistema.

#### **Perfil de Hardware e Sistema Operacional**
* **Hardware:** Modelo da CPU, quantidade de memória RAM, layout dos discos e partições, interfaces de rede.
* **Sistema Operacional:** Distribuição e versão do SO, versão do kernel, e o nível de patch/atualização.

#### **Perfil de Software e Aplicações**
* **Softwares Instalados:** Uma lista completa de todos os pacotes e aplicações instalados.
* **Serviços em Execução:** Quais daemons ou serviços estão configurados para iniciar com o sistema e quais estão atualmente em execução.

#### **Perfil de Rede (Crucial para a Segurança)**
* **Portas em Escuta (Listening Ports):** Um mapa de todas as portas TCP e UDP que estão abertas e escutando por conexões, e qual processo está associado a cada uma. Qualquer porta aberta que não esteja na linha de base é um ponto de investigação imediato.
* **Configuração de Rede:** Endereço IP, máscara, gateway, servidores DNS.
* **Regras de Firewall:** Um snapshot das regras ativas do firewall do host (como `iptables` ou `UFW`).

#### **Perfil de Contas e Acessos**
* **Contas de Usuário:** Uma lista de todas as contas de usuário locais e de rede que têm permissão para acessar o servidor.
* **Privilégios:** Quais usuários possuem privilégios elevados (como acesso `sudo`).

#### **Perfil de Performance**
* **Métricas:** CPU (uso médio/pico), Memória (uso/disponível), Disco (espaço livre, I/O), Rede (tráfego de entrada/saída).

---

### 3. Ferramentas e Técnicas para o Perfilamento

O perfilamento pode ser realizado com uma combinação de comandos nativos e ferramentas especializadas.

* **Comandos Nativos do Linux:**
    * Para listar softwares: `dpkg -l` (Debian/Ubuntu) ou `rpm -qa` (Red Hat/CentOS).
    * Para listar serviços: `systemctl list-units --type=service`.
    * Para listar portas em escuta: `ss -lntp` ou `netstat -lntp`.
    * Para verificar usuários: `cat /etc/passwd`.
    * Para métricas de performance: `top`, `htop`, `vmstat`, `iostat`.

* **Ferramentas de Monitoramento Contínuo:** Para que a linha de base seja útil, ela precisa ser comparada com o estado atual. Ferramentas como **Zabbix, Nagios ou Prometheus com Grafana** são usadas para coletar e visualizar as métricas de performance continuamente.

* **Sistemas de Gerenciamento de Configuração:** Ferramentas como **Ansible, Puppet e Chef** são usadas não apenas para coletar informações, mas para **definir e impor** a linha de base de configuração, garantindo que os servidores permaneçam em um estado conhecido e seguro.

---

### 4. O Processo na Prática

1.  **Construção e Endurecimento (Hardening):** O perfilamento ideal começa com um servidor recém-instalado e "endurecido" (hardened), onde todas as configurações de segurança iniciais foram aplicadas.
2.  **Coleta da Linha de Base Inicial:** Execute os comandos e ferramentas para capturar o estado "saudável" e conhecido do servidor. Documente rigorosamente todos os resultados.
3.  **Monitoramento Contínuo:** Configure ferramentas automatizadas para monitorar as principais métricas de performance e segurança (como integridade de arquivos) em relação à linha de base.
4.  **Revisão e Atualização:** Uma linha de base não é estática. Ela deve ser formalmente revisada e atualizada após qualquer mudança controlada significativa, como a instalação de um novo software ou uma grande atualização do sistema.

### Conclusão

O perfilamento de servidores é a transição de uma postura de segurança reativa para uma proativa. Em vez de simplesmente procurar por "coisas ruins" conhecidas, os analistas ganham a capacidade de detectar "coisas diferentes" do normal. Um perfil bem definido e mantido é uma das ferramentas mais poderosas à disposição de uma equipe de segurança e operações, transformando a complexidade de um servidor em um estado conhecido, monitorável e, acima de tudo, defensável.