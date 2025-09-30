# Servidores AAA
## Introdução

À medida que uma rede cresce, de um punhado de dispositivos para dezenas, centenas ou milhares de roteadores, switches, firewalls e pontos de acesso, o gerenciamento de quem pode acessá-los e o que podem fazer se torna uma tarefa hercúlea e propensa a erros. Gerenciar contas de usuário e senhas localmente em cada dispositivo é insustentável e inseguro.

A solução para este desafio é a centralização, implementada através de um **Servidor AAA**. O acrônimo AAA representa os três pilares do controle de acesso à rede:

1.  **Authentication (Autenticação):** "Quem é você?" - O processo de verificar a identidade.
2.  **Authorization (Autorização):** "O que você pode fazer?" - O processo de aplicar permissões.
3.  **Accounting (Contabilização):** "O que você fez?" - O processo de registrar as ações.

Um servidor AAA é o sistema centralizado que fornece esses três serviços, atuando como o cérebro da política de segurança de acesso para toda a infraestrutura de rede.

---

### 1. Os Protocolos AAA: RADIUS vs. TACACS+

A comunicação entre um dispositivo de rede (como um roteador ou VPN) e o servidor AAA é realizada através de protocolos específicos. Os dois mais proeminentes na indústria são RADIUS e TACACS+.

#### **RADIUS (Remote Authentication Dial-In User Service)**
* **Origem:** Um padrão aberto e antigo, amplamente suportado por praticamente todos os fabricantes de rede.
* **Transporte:** Utiliza o protocolo **UDP**, que é rápido, mas não garante a entrega de pacotes.
* **Segurança:** Criptografa **apenas a senha** do usuário no pacote de requisição. O resto das informações, como o nome de usuário e outros atributos, é enviado em texto claro.
* **Funcionalidade:** Combina os processos de Autenticação e Autorização em uma única etapa. A Contabilização é um processo separado.
* **Caso de Uso Principal:** **Autenticação de acesso à rede por usuários finais**. É o protocolo padrão para 802.1X (segurança de portas em redes cabeadas e Wi-Fi) e para a maioria das autenticações de VPN.

#### **TACACS+ (Terminal Access Controller Access-Control System Plus)**
* **Origem:** Um protocolo proprietário da Cisco, mas cujas especificações são abertas e amplamente adotadas.
* **Transporte:** Utiliza o protocolo **TCP**, que é orientado à conexão e garante a entrega confiável das mensagens.
* **Segurança:** Criptografa **todo o corpo do pacote**, oferecendo uma confidencialidade muito superior à do RADIUS.
* **Funcionalidade:** Separa completamente os três pilares do AAA. A Autenticação, a Autorização e a Contabilização são processos distintos e independentes.
* **Caso de Uso Principal:** **Gerenciamento de acesso de administradores a dispositivos de rede**. A separação do AAA é sua grande vantagem, permitindo um controle de autorização extremamente granular. Por exemplo, é possível criar uma política onde um "Administrador Júnior" pode se autenticar e executar apenas comandos de visualização (`show`), enquanto um "Administrador Sênior" pode executar comandos de configuração (`configure terminal`).

#### **Tabela Comparativa**

| Característica | RADIUS | TACACS+ |
| :--- | :--- | :--- |
| **Transporte** | UDP (Portas 1812/1813 ou 1645/1646) | TCP (Porta 49) |
| **Criptografia** | Apenas a senha | Corpo inteiro do pacote |
| **Separação AAA** | Autenticação e Autorização combinadas | Processos de AAA separados |
| **Principal Caso de Uso**| Acesso de usuário à rede (802.1X, VPN) | Acesso de administrador a dispositivos |

---

### 2. O Fluxo de Trabalho de uma Autenticação AAA

Para entender como um servidor AAA funciona na prática, vamos usar o cenário de um funcionário se conectando ao Wi-Fi corporativo:

1.  **Requisição (Supplicant):** O laptop do funcionário ("suplicante") solicita a conexão ao Ponto de Acesso (Access Point - AP) Wi-Fi e fornece suas credenciais (usuário e senha).
2.  **Mediação (Authenticator):** O AP atua como o "autenticador" ou cliente AAA. Ele **não** armazena as senhas dos usuários. Em vez disso, ele encapsula as credenciais em um pacote **RADIUS** e o encaminha para o endereço IP do servidor AAA central.
3.  **Decisão (AAA Server):** O servidor AAA recebe o pacote RADIUS. Ele abre o pacote, descriptografa a senha e a compara com sua base de dados (que pode ser local ou integrada a um diretório como o Active Directory).
4.  **Resposta:** Com base na verificação, o servidor AAA envia uma de duas respostas ao AP:
    * **`Access-Accept`:** Acesso permitido. A resposta pode incluir atributos de autorização, como "coloque este usuário na VLAN 20 (Vendas)".
    * **`Access-Reject`:** Acesso negado.
5.  **Aplicação da Política:** O AP recebe a resposta do servidor AAA e executa a decisão: ou ele permite que o laptop do funcionário se conecte à rede (na VLAN correta), ou ele bloqueia a conexão.
6.  **Contabilização:** Assim que a sessão se inicia, o AP envia uma mensagem `Accounting-Start` para o servidor AAA. Quando o funcionário se desconecta, ele envia uma mensagem `Accounting-Stop`, permitindo a auditoria completa da sessão.

---

### 3. Implementações Comuns

Existem várias soluções de software que podem funcionar como um servidor AAA, incluindo:

* **Microsoft NPS (Network Policy Server):** O servidor RADIUS integrado ao Windows Server.
* **Cisco ISE (Identity Services Engine):** Uma plataforma de controle de acesso de última geração e muito poderosa.
* **FreeRADIUS:** O servidor RADIUS de código aberto mais popular e amplamente utilizado do mundo.

### Conclusão

Os servidores AAA são o pilar do controle de acesso em redes modernas e escaláveis. Ao centralizar as decisões de autenticação, autorização e o registro de atividades, eles resolvem os imensos desafios de segurança e gerenciamento de manter contas de usuário em centenas de dispositivos de rede individuais. Compreender as diferenças e os casos de uso dos protocolos RADIUS e TACACS+ é essencial para qualquer profissional de segurança de rede encarregado de projetar e manter um acesso seguro e auditável à infraestrutura digital.