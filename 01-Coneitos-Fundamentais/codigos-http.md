# Códigos de Status HTTP

## Introdução

Toda interação na World Wide Web é um diálogo entre um cliente (geralmente um navegador) e um servidor. O cliente faz uma requisição (ex: "GET /pagina.html"), e o servidor responde. A parte mais crucial dessa resposta é o **código de status HTTP**, um número de três dígitos que informa ao cliente o resultado de sua solicitação.

Esses códigos são organizados em cinco classes, identificadas pelo primeiro dígito. Entender essas classes e os códigos dentro delas é essencial para desenvolvedores, administradores de sistemas e, especialmente, para analistas de cibersegurança, que os utilizam para diagnosticar problemas, identificar ataques de reconhecimento e analisar logs em busca de atividades maliciosas.

---

### Classe 1xx: Respostas de Informação

Estes códigos indicam uma resposta provisória. O servidor recebeu os cabeçalhos da requisição e o cliente pode continuar. Raramente são vistos em navegação normal, sendo mais utilizados em nível de protocolo.

| Código | Nome Oficial | Descrição |
| :--- | :--- | :--- |
| **100** | Continue | O servidor recebeu os cabeçalhos da requisição e o cliente deve proceder com o envio do corpo da requisição. |
| **101** | Switching Protocols | O servidor está mudando de protocolo, conforme solicitado pelo cliente (ex: upgrade de HTTP para WebSocket). |
| **102** | Processing (WebDAV) | O servidor recebeu e está processando a requisição, mas ainda não há uma resposta final. |

---

### Classe 2xx: Sucesso

Esta classe indica que a requisição do cliente foi recebida, compreendida e aceita com sucesso.

| Código | Nome Oficial | Descrição |
| :--- | :--- | :--- |
| **200** | OK | A requisição foi bem-sucedida. É o código de sucesso mais comum. |
| **201** | Created | A requisição foi bem-sucedida e um novo recurso foi criado como resultado (ex: após um POST ou PUT). |
| **202** | Accepted | A requisição foi aceita para processamento, mas o processamento não foi concluído. |
| **203** | Non-Authoritative Information | A requisição foi bem-sucedida, mas as informações retornadas podem ser de uma cópia local ou de terceiros. |
| **204** | No Content | O servidor processou a requisição com sucesso, mas não há conteúdo para retornar (ex: após um `DELETE`). |
| **205** | Reset Content | O servidor processou a requisição e solicita que o cliente reinicie a visualização do documento. |
| **206** | Partial Content | O servidor está entregando apenas parte do recurso, comum em downloads ou streaming. |
| **Nota de Segurança:** | Um código **200 OK** em resposta a uma requisição maliciosa (ex: em um ataque de Blind SQL Injection) pode ser o sinal que o atacante espera para confirmar que a vulnerabilidade existe. |

---

### Classe 3xx: Redirecionamento

Esta classe indica que o cliente precisa tomar uma ação adicional para completar a requisição.

| Código | Nome Oficial | Descrição |
| :--- | :--- | :--- |
| **300** | Multiple Choices | A requisição tem mais de uma resposta possível. O cliente deve escolher uma. |
| **301** | Moved Permanently | O recurso solicitado foi movido permanentemente para uma nova URL. |
| **302** | Found | O recurso está temporariamente em uma URL diferente. (Anteriormente "Moved Temporarily"). |
| **303** | See Other | A resposta pode ser encontrada em outra URL usando o método GET. |
| **304** | Not Modified | Resposta de cache. O recurso não foi modificado desde a última requisição, então o cliente pode usar sua versão em cache. |
| **307** | Temporary Redirect | Semelhante ao 302, mas não permite que o método HTTP seja alterado. |
| **308** | Permanent Redirect | A versão permanente do 307. |
| **Nota de Segurança:** | Redirecionamentos (especialmente 302) são usados em ataques para levar o usuário através de uma cadeia de sites até uma página maliciosa. Vulnerabilidades de **Open Redirect** em um site podem ser abusadas por phishers. |

---

### Classe 4xx: Erro do Cliente

Esta classe indica que a requisição não pôde ser atendida porque o cliente parece ter cometido um erro.

| Código | Nome Oficial | Descrição |
| :--- | :--- | :--- |
| **400** | Bad Request | O servidor não pôde entender a requisição devido a uma sintaxe inválida. |
| **401** | Unauthorized | A requisição exige autenticação. O cliente precisa se autenticar para obter a resposta. |
| **402** | Payment Required | Reservado para uso futuro. |
| **403** | Forbidden | O servidor entendeu a requisição, mas se recusa a autorizá-la. O cliente não tem direitos de acesso. |
| **404** | Not Found | O servidor não encontrou o recurso solicitado. É o erro mais famoso da web. |
| **405** | Method Not Allowed | O método de requisição (ex: POST) não é permitido para o recurso solicitado. |
| **406** | Not Acceptable | O servidor não pode gerar um conteúdo que corresponda aos critérios aceitáveis pelo cliente. |
| **408** | Request Timeout | O servidor expirou o tempo de espera pela requisição do cliente. |
| **409** | Conflict | A requisição não pôde ser completada devido a um conflito com o estado atual do recurso. |
| **410** | Gone | O recurso solicitado não está mais disponível no servidor e não há endereço de encaminhamento. |
| **429** | Too Many Requests| O usuário enviou muitas requisições em um determinado período de tempo (rate-limiting). |
| **Nota de Segurança:** | A classe 4xx é **extremamente útil para um atacante** em fase de reconhecimento. Um `404 Not Found` em `/admin.php` diz que a página não existe, enquanto um `403 Forbidden` diz que a página **existe**, mas o acesso é restrito. Analisar os códigos 4xx ajuda a mapear a estrutura e as proteções de um site. Um pico de erros 401/403 nos logs pode indicar um ataque de força bruta em andamento. |

---

### Classe 5xx: Erro do Servidor

Esta classe indica que o servidor falhou em atender a uma requisição aparentemente válida.

| Código | Nome Oficial | Descrição |
| :--- | :--- | :--- |
| **500** | Internal Server Error | Uma mensagem genérica para uma condição inesperada que impediu o servidor de atender à requisição. |
| **501** | Not Implemented | O servidor não suporta a funcionalidade necessária para atender à requisição. |
| **502** | Bad Gateway | O servidor, atuando como um gateway ou proxy, recebeu uma resposta inválida do servidor upstream. |
| **503** | Service Unavailable | O servidor não está pronto para lidar com a requisição (ex: está sobrecarregado ou em manutenção). |
| **504** | Gateway Timeout | O servidor, atuando como um gateway, não recebeu uma resposta a tempo do servidor upstream. |
| **505** | HTTP Version Not Supported| A versão do protocolo HTTP usada na requisição não é suportada pelo servidor. |
| **Nota de Segurança:** | Um erro **500 Internal Server Error**, especialmente se mal configurado, pode vazar informações sensíveis sobre a infraestrutura do servidor (como versões de software, caminhos de arquivos, trechos de código ou queries de banco de dados), que são valiosas para um atacante. Isso é conhecido como **Improper Error Handling**. |

### Conclusão

Os códigos de status HTTP são a linguagem fundamental da comunicação na web. Para um analista de segurança, eles são mais do que apenas mensagens de erro ou sucesso; são **indicadores**. Um fluxo de códigos 200 em um log pode ser normal, mas um pico de 403 pode ser uma tentativa de acesso não autorizado. Uma enxurrada de 404 pode ser um scanner procurando por diretórios ocultos. E um aumento de 500 pode ser o resultado de um ataque de injeção de SQL bem-sucedido. Dominar o significado desses códigos é essencial para traduzir os logs brutos de um servidor web em uma narrativa clara sobre sua saúde e segurança.