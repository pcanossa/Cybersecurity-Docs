# Vulnerabilidades do Protocolo TCP

**Data de Publicação:** 11 de Agosto de 2025  
**Autora:** Patrícia Canossa Gagliardi

## Introdução

O Protocolo de Controle de Transmissão (TCP) é o alicerce da comunicação confiável na internet. Diferente de protocolos "dispare e esqueça" como o UDP, o TCP é **orientado à conexão** e **confiável**. Ele garante que os dados cheguem em ordem e sem erros através de dois mecanismos principais: o *handshake* de três vias (*three-way handshake*) para estabelecer uma conexão, e o uso de números de sequência para ordenar e confirmar o recebimento de pacotes. Paradoxalmente, são exatamente essas características de gerenciamento de **estado** e **confiança** na sequência de pacotes que dão origem às suas vulnerabilidades mais significativas. Este artigo detalha os três principais vetores de ataque que exploram o design fundamental do TCP.

---

### 1. Ataque à Disponibilidade: A Inundação de SYN (SYN Flood)

Este é um dos ataques de Negação de Serviço (DoS) mais antigos e eficazes, visando diretamente o processo de estabelecimento de conexão do TCP.

* **O Alvo: O Handshake de Três Vias:** Uma conexão TCP legítima é estabelecida com um "aperto de mãos" de três etapas:
    1.  `Cliente -> [SYN] -> Servidor`
    2.  `Servidor -> [SYN/ACK] -> Cliente`
    3.  `Cliente -> [ACK] -> Servidor`

* **O Mecanismo do Ataque:** O atacante explora o momento em que o servidor está aguardando o passo 3.
    1.  O adversário envia um volume massivo de pacotes `SYN` para o servidor alvo.
    2.  Crucialmente, o endereço IP de origem em cada um desses pacotes é **falsificado (spoofed)**, apontando para um host inexistente ou que não responderá.
    3.  O servidor recebe cada `SYN`, aloca uma parte de sua memória para a nova conexão (colocando-a em uma fila de "conexões semiabertas" no estado `SYN_RECEIVED`) e envia o `SYN/ACK` de volta para o endereço falsificado.
    4.  Como o `ACK` final nunca chega, as conexões semiabertas permanecem na fila do servidor, aguardando um timeout. O ataque envia pacotes `SYN` mais rápido do que as conexões pendentes expiram.
    5.  **Resultado:** A fila de conexões do servidor (backlog) fica completamente cheia. Qualquer tentativa de conexão de um usuário legítimo é descartada, pois o servidor não tem mais recursos para aceitá-la, resultando em negação de serviço.

* **Estratégias de Mitigação:**
    * **SYN Cookies:** A defesa mais elegante. O servidor, ao receber um `SYN`, responde com um `SYN/ACK` contendo um número de sequência especialmente criado (o "cookie") que codifica os detalhes da conexão. Ele não aloca memória. Apenas quando o cliente envia o `ACK` final, contendo o cookie correto, é que o servidor valida a conexão e aloca os recursos.
    * **Firewalls e IPS:** Dispositivos de segurança modernos são capazes de detectar os padrões de um SYN Flood e mitigar o ataque antes que ele chegue ao servidor.

---

### 2. Ataque à Integridade da Conexão: O Reset Forçado (TCP Reset)

Enquanto o encerramento normal de uma conexão TCP é um processo gracioso de quatro vias (usando flags `FIN`), o flag `RST` (Reset) existe para terminar uma conexão de forma abrupta e imediata.

* **O Mecanismo do Ataque:** Um adversário pode injetar um pacote TCP forjado na comunicação entre dois hosts para encerrá-la prematuramente.
    * **O Desafio:** Para que o pacote `RST` seja considerado válido pela vítima, ele não pode ser um pacote qualquer. O atacante precisa forjar um pacote com a combinação exata de: `IP de Origem`, `Porta de Origem`, `IP de Destino` e `Porta de Destino`. Além disso, e mais importante, o **número de sequência** do pacote `RST` deve estar dentro da "janela de recepção" esperada pelo host de destino.
    * **Resultado:** Se o atacante for bem-sucedido, a vítima aceita o pacote `RST` e encerra sua ponta da conexão instantaneamente. Isso pode ser usado para interromper seletivamente comunicações críticas, como sessões de roteamento BGP ou transações de banco de dados.

* **Estratégias de Mitigação:** A principal defesa é dificultar a adivinhação dos números de sequência. O uso de protocolos de criptografia na camada de rede (IPsec) ou transporte (TLS) pode autenticar os pacotes, tornando impossível a injeção de um pacote forjado por um terceiro não autorizado.

---

### 3. Ataque à Autenticidade: O Sequestro de Sessão (TCP Session Hijacking)

Este ataque clássico visa assumir uma sessão TCP já estabelecida e autenticada, permitindo que o atacante se passe por um usuário legítimo.

* **O Mecanismo Clássico:**
    1.  O atacante identifica e monitora uma sessão ativa entre um cliente e um servidor.
    2.  Ele "silencia" o cliente legítimo, geralmente com um ataque de DoS.
    3.  O atacante então começa a se comunicar com o servidor, falsificando o endereço IP do cliente.
    4.  **O Desafio Central:** Para que a comunicação funcione, o atacante precisa adivinhar com precisão o próximo **número de sequência** que o servidor espera receber do cliente. Cada pacote enviado pelo atacante deve ter o número de sequência correto para ser aceito.

* **Contexto Moderno:** Este ataque, em sua forma pura, é hoje em grande parte teórico. No início da internet, os Números de Sequência Iniciais (ISNs) eram previsíveis. Hoje, todos os sistemas operacionais modernos implementam uma forte **randomização dos ISNs**, tornando a previsão dos números de sequência em uma janela de tempo útil praticamente impossível. O termo "sequestro de sessão" hoje se refere mais comumente a ataques na Camada de Aplicação, como o roubo de cookies de sessão via XSS ou MitM.

* **Estratégias de Mitigação:** A defesa que tornou este ataque obsoleto foi a randomização de ISNs implementada nos sistemas operacionais. A adoção universal da criptografia via **TLS (HTTPS)** é a defesa definitiva, pois toda a sessão TCP, incluindo seus números de sequência, é criptografada e se torna invisível para um observador externo.

### Conclusão

As vulnerabilidades do TCP nascem de suas maiores forças: sua capacidade de criar e manter conexões estado-financiado (stateful) e confiáveis. A história dos ataques ao TCP e suas respectivas mitigações: SYN Cookies, ISNs randomizados e a onipresença da criptografia, ilustra perfeitamente a "corrida armamentista" da cibersegurança. Cada fraqueza explorada no design de um protocolo leva ao desenvolvimento de novas defesas engenhosas, resultando em uma internet mais segura e resiliente.