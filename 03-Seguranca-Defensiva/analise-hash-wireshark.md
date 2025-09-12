# Investigação de Malware em Rede com Wireshark

## Introdução

Este guia prático detalha um fluxo de trabalho fundamental para a triagem de alertas de malware baseados em rede. Seguiremos um processo de quatro passos para ir do alerta inicial a um veredito baseado em evidências, utilizando ferramentas padrão da indústria como o Wireshark e a análise de reputação de arquivos.

**Ferramentas Necessárias:**
* Acesso a um console SIEM.
* Software de análise de pacotes (Wireshark).
* Acesso a um terminal (Linux, macOS ou Windows com PowerShell).

---

### Passo 1: Contextualizar o Alerta e Iniciar a Análise de Pacotes

A primeira fase é entender o alerta e encontrar a evidência bruta.

1.  **Receber e Interpretar o Alerta:** A sua investigação começa com um alerta do IPS, apresentado pelo SIEM, referenciando um endereço IP local específico, como 10.8.19.101. Anote as informações chave: IP de origem/destino, timestamp e a assinatura do IPS que foi acionada.

2.  **Pivotar para o Wireshark:** Para validar o alerta, você precisa examinar o tráfego que o causou. Obtenha a captura de pacotes (`.pcap`) correspondente ao momento do alerta.

3.  **Filtrar o Tráfego:** Abra a captura no Wireshark. Para focar na atividade relevante, use um filtro de exibição. No campo de filtro, digite `ip.addr == 10.8.19.101` e pressione Enter. Isso mostrará apenas os pacotes enviados ou recebidos por aquele host.

---

### Passo 2: Extrair o Artefato Suspeito da Rede

Com o tráfego isolado, o próximo objetivo é encontrar e extrair qualquer arquivo que possa ter sido transferido.

1.  **Identificar a Transferência:** Ao analisar os pacotes filtrados, você percebe que um arquivo foi baixado pelo host. Em tráfego web, isso geralmente é visível como uma requisição `HTTP GET` seguida por uma resposta `HTTP/1.1 200 OK` que contém os dados do arquivo.

2.  **Exportar o Objeto:** O Wireshark pode remontar automaticamente o arquivo a partir dos pacotes TCP.
    * No menu, vá para `Arquivo > Exportar Objetos > HTTP...`.
    * O Wireshark exibirá uma lista de todos os objetos HTTP transferidos na captura.
    * Selecione o arquivo suspeito na lista.
    * Clique em "Salvar Como..." e salve o arquivo em uma pasta de análise segura com um nome de referência, como `ooiwy.pdf`.

---

### Passo 3: Gerar a Impressão Digital (Hash SHA256)

Antes de enviar o arquivo para qualquer lugar, você precisa criar um identificador único e seguro para ele.

1.  **Abrir o Terminal:** Navegue até o diretório onde você salvou o arquivo.

2.  **Executar o Comando de Hashing:** Use o comando apropriado para o seu sistema operacional para gerar o valor de hash SHA256 do arquivo.

    * **No Linux:**
      ```bash
      sha256sum ooiwy.pdf
      ```
      **Saída de exemplo:** `f25a780095730701efac67e9d5b84bc289afea56d96d8aff8a44af69ae606404  ooiwy.pdf`

    * **No Windows (PowerShell):**
      ```powershell
      Get-FileHash .\ooiwy.pdf -Algorithm SHA256
      ```

    * **No macOS:**
      ```bash
      shasum -a 256 ooiwy.pdf
      ```

3.  **Copiar o Hash:** A longa sequência de caracteres retornada é a "impressão digital" do arquivo. Copie este valor.

---

### Passo 4: Validar a Reputação e Chegar a um Veredito

Agora você usará o hash para consultar a inteligência de ameaças global e determinar se o arquivo é malicioso.

1.  **Acessar um Site de Reputação:** Abra seu navegador e acesse um serviço de reputação de arquivos (o mais conhecido é o VirusTotal).

2.  **Submeter o Hash:** Cole o hash SHA256 que você copiou no campo de busca do site. Esta ação não envia o arquivo, apenas sua impressão digital. Este método é usado para validar a sequência e ver se o arquivo é um malware conhecido.

3.  **Analisar o Resultado e Decidir:**
    * **Se o resultado for POSITIVO (ex: "50/70 motores detectaram"):** O arquivo é um malware conhecido. O alerta do IPS é um **Verdadeiro Positivo**. Sua próxima ação é escalar o incidente para a equipe de Resposta a Incidentes (Nível 2), fornecendo todas as evidências que você coletou: o IP do host, o hash do arquivo e o nome da família do malware.
    * **Se o resultado for NEGATIVO (ex: "0/70 motores detectaram"):** O hash não é conhecido. Isso pode significar duas coisas:
        * O alerta do IPS foi um **Falso Positivo** e o arquivo é benigno.
        * O arquivo é uma ameaça nova ou direcionada (**Zero-Day**) e ainda não foi catalogado.
        Neste caso, o próximo passo seria uma análise mais profunda, como submeter o **arquivo em si** para uma análise de comportamento em um ambiente de sandbox.

### Conclusão

Seguindo estes quatro passos, você transformou um alerta de rede de baixo contexto em uma conclusão clara e baseada em evidências. Este processo de **Alertar -> Capturar -> Extrair -> Hashear -> Validar** é um fluxo de trabalho essencial e repetível que constitui a base da triagem de incidentes em um SOC, permitindo uma resposta rápida, precisa e eficaz às ameaças de segurança.