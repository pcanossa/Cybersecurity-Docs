# Vulnerabilidades do DHCP 

**Data de Publicação:** 13 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução

O Protocolo de Configuração Dinâmica de Host (DHCP) é um dos heróis não celebrados das redes modernas. Ele elimina a necessidade de configuração manual de endereços IP em cada dispositivo, automatizando a atribuição de IPs, máscaras de sub-rede, gateways padrão e servidores DNS. Essa funcionalidade "plug-and-play" é o que permite que redes, de pequenos escritórios a grandes corporações, escalem com facilidade. No entanto, assim como outros protocolos fundamentais como o ARP, o DHCP foi projetado para operar em um ambiente de confiança implícita. Ele não possui mecanismos de autenticação robustos, o que o torna vulnerável a ataques de impersonação e negação de serviço que podem paralisar ou comprometer totalmente a segurança de uma rede local.

---

### 1. O Processo DORA: O Funcionamento Legítimo do DHCP

Para entender a falha, é preciso entender o processo. A atribuição de um endereço via DHCP segue um processo de quatro etapas, conhecido pelo acrônimo **DORA**:

1.  **Discover (Descoberta):** Um novo cliente na rede envia uma mensagem `DHCPDISCOVER` em broadcast, perguntando: "Existe algum servidor DHCP que possa me atender?".
2.  **Offer (Oferta):** Todos os servidores DHCP que recebem a mensagem respondem com um `DHCPOFFER`, que é uma proposta de parâmetros de configuração (IP, máscara, etc.).
3.  **Request (Requisição):** O cliente recebe uma ou mais ofertas e escolhe uma (tipicamente, a primeira que chega). Ele então envia uma mensagem `DHCPREQUEST` em broadcast, informando a todos os servidores qual oferta ele decidiu aceitar.
4.  **Acknowledgment (Confirmação):** O servidor cuja oferta foi escolhida envia um `DHCPACK` final, confirmando o "aluguel" (lease) do endereço IP e dos outros parâmetros, finalizando o processo.

---

### 2. Ataque de Falsificação (DHCP Spoofing)

Este é o ataque mais comum e perigoso contra o DHCP, visando um ataque Man-in-the-Middle (MitM).

* **O Mecanismo do Ataque:** Um adversário conecta um servidor DHCP não autorizado ("rogue") à rede. Este servidor falso escuta as mensagens `DHCPDISCOVER` dos clientes. O sucesso do ataque depende de uma simples "corrida": o servidor do atacante precisa enviar sua `DHCPOFFER` maliciosa para o cliente **antes** que o servidor DHCP legítimo o faça. Como o cliente aceita a primeira oferta que recebe, ele cai na armadilha.

* **As Consequências Maliciosas:** A oferta do atacante contém informações de configuração falsas que redirecionam o tráfego da vítima:
    * **Gateway Padrão Falso:** O atacante configura seu próprio IP como o gateway da vítima. Como resultado, todo o tráfego da vítima destinado a outras redes (como a internet) é enviado primeiro para a máquina do atacante, permitindo que ele capture, analise e modifique os dados.
    * **Servidor DNS Falso:** O atacante configura seu próprio IP como o servidor DNS. Isso lhe dá controle total sobre a resolução de nomes da vítima, permitindo-lhe redirecionar sites legítimos (como `banco.com.br`) para servidores de phishing, bloquear o acesso a sites específicos ou realizar outros ataques baseados em DNS.
    * **Endereço IP Inválido:** Em um cenário mais simples de Negação de Serviço (DoS), o atacante pode fornecer um endereço IP ou gateway inválido, impedindo que a vítima se comunique na rede.

---

### 3. Ataque de Esgotamento (DHCP Starvation)

Este é um ataque de DoS direcionado não ao cliente, mas ao próprio servidor DHCP legítimo. Frequentemente, é usado como um passo preparatório para um ataque de spoofing.

* **O Mecanismo do Ataque:** O atacante utiliza uma ferramenta para inundar a rede com um grande número de pacotes `DHCPDISCOVER`. O detalhe crucial é que cada uma dessas requisições utiliza um endereço MAC de origem forjado e único.
* **O Resultado:** O servidor DHCP legítimo recebe essa enxurrada de requisições. Para cada uma, ele reserva um endereço IP de seu pool disponível e o associa ao MAC falsificado, aguardando a conclusão do processo DORA. Como o atacante nunca completa os passos de Requisição e Confirmação, o servidor fica com seu pool de endereços completamente exaurido, "alugado" para clientes fantasmas.
* **O Ataque Combinado:** Uma vez que o servidor legítimo está "faminto" (*starved*) e não tem mais IPs para oferecer, o atacante ativa seu servidor DHCP falso. Agora, qualquer novo cliente na rede será **obrigatoriamente** servido pelo atacante, garantindo o sucesso do ataque de spoofing.

---

### 4. Estratégias de Mitigação

A defesa contra os ataques ao DHCP é implementada na infraestrutura de rede, especificamente nos switches de Camada 2.

* **DHCP Snooping:** Esta é a principal e mais eficaz contramedida.
    * **Conceito:** O DHCP Snooping é uma funcionalidade de segurança que permite ao switch analisar o tráfego DHCP e diferenciar entre fontes legítimas e não autorizadas.
    * **Implementação:** O administrador de rede configura as portas do switch como **confiáveis (trusted)** ou **não confiáveis (untrusted)**.
        * **Portas Confiáveis:** Portas que se conectam a servidores DHCP legítimos.
        * **Portas Não Confiáveis:** Todas as outras portas, onde se conectam os dispositivos finais (desktops, laptops, etc.).
    * **Funcionamento:** O switch inspeciona as mensagens DHCP. Ele só permitirá que mensagens de servidor (`DHCPOFFER`, `DHCPACK`) passem através de portas marcadas como **confiáveis**. Se um atacante conectar um servidor rogue a uma porta de usuário (não confiável) e tentar enviar uma oferta, o switch detectará a mensagem, a descartará imediatamente e poderá registrar uma violação de segurança.
    * **Benefício Adicional:** Ao inspecionar o tráfego, o DHCP Snooping cria uma tabela de "amarração" (binding table) que mapeia o MAC address, o endereço IP alugado e a porta do switch para cada cliente. Essa tabela é usada por outras funcionalidades de segurança, como a **Inspeção Dinâmica de ARP (DAI)**, para prevenir ataques de ARP Poisoning.

### Conclusão

O DHCP é um protocolo de conveniência e automação cuja eficiência deriva de sua confiança inerente no ambiente de rede local. Ataques como o Spoofing e o Starvation exploram essa confiança para comprometer a integridade e a disponibilidade da rede. A solução para essas vulnerabilidades não está em modificar o protocolo em si, mas em fortalecer a infraestrutura sobre a qual ele opera. Ao habilitar a inteligência nos switches de rede com funcionalidades como o DHCP Snooping, as organizações podem aplicar uma camada de validação e controle, garantindo que a automação da rede não se torne uma porta de entrada para o adversário.