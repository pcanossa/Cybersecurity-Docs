**Passo 1: Verifique se Você Já Tem uma Chave SSH 🔑**


Primeiro, vamos ver se já existe uma chave no seu computador. Abra o terminal e digite:




```Bash
ls -al \~/.ssh
```



Procure por arquivos com nomes como id\_rsa.pub, id\_ecdsa.pub ou **id\_ed25519.pub**. Se encontrar um desses, pule para o **Passo 3**.


**Passo 2: Gere uma Nova Chave SSH (se necessário)**


Se você não encontrou nenhum arquivo de chave pública, crie um novo. O método ed25519 é o mais recomendado atualmente. Substitua o email pelo seu.




```Bash
ssh-keygen -t ed25519 -C "seu\_email@exemplo.com"
```



Quando ele perguntar "Enter a file in which to save the key", apenas pressione **Enter** para aceitar o local padrão. É recomendado que você crie uma senha (passphrase) para a sua chave quando solicitado, pois isso a torna mais segura.


**Passo 3: Adicione a Chave SSH ao seu GitHub 🔗**


Agora, você precisa copiar sua chave **pública** e adicioná-la à sua conta do GitHub.



1.  **Copie a chave pública.** Use o comando abaixo. Se você criou um tipo de chave diferente, mude o nome do arquivo.
   
    ```Bash
    cat \~/.ssh/id\_ed25519.pub
    ```

    Isso irá exibir a chave no terminal. Copie toda a saída, começando com ssh-ed25519 e terminando com seu email.

2.  **Acesse o GitHub:**


    *   Vá para [github.com](https://github.com) e faça login.

    *   Clique na sua foto de perfil no canto superior direito e vá em **Settings**.

    *   No menu esquerdo, clique em **SSH and GPG keys**.

    *   Clique no botão verde **New SSH key**.

    *   Dê um **Title** para a chave (por exemplo, "Meu Notebook Pessoal").

    *   Cole a chave que você copiou no campo **Key**.

    *   Clique em **Add SSH key**.


**Passo 4: Teste a Conexão ✅**


Para verificar se tudo funcionou, use o comando:

```Bash
ssh -T git@github.com
```

Você poderá ver um aviso sobre a autenticidade do host. Digite yes e pressione Enter. Se tudo estiver correto, você verá uma mensagem como: Hi USERNAME\! You've successfully authenticated....



Agora, tente o comando git push novamente. Ele deve funcionar\!



**Alternativa Rápida: Usar HTTPS**


Se você não quiser configurar o SSH, pode mudar a URL do seu repositório para usar HTTPS. Com HTTPS, você fará a autenticação com seu nome de usuário e um **Personal Access Token** (Token de Acesso Pessoal) em vez da senha.



1.  **Verifique a URL atual:**
   
    ```Bash
    git remote -v
    ```

    A saída provavelmente mostrará uma URL começando com git@github.com:.

2.  Mude para HTTPS:
    Substitua USERNAME e REPO pelo seu nome de usuário e nome do repositório.

    ```Bash
    git remote set-url origin https://github.com/USERNAME/REPO.git
    ```


Agora, ao dar git push, ele pedirá seu nome de usuário e o token de acesso pessoal em vez da sua senha.