# My Auth Redirect - Ponte para Supabase e Streamlit

Este repositório contém uma única página `index.html` que serve como uma ponte para o fluxo de redefinição de senha entre o Supabase e uma aplicação Streamlit.

## O Problema

O Supabase, ao enviar um link de redefinição de senha, retorna os tokens de autenticação (`access_token`, `refresh_token`) no **fragmento** da URL (a parte que vem depois do `#`).

No entanto, o Streamlit não consegue ler o fragmento da URL, apenas os **parâmetros de busca** (a parte que vem depois do `?`). Isso impede que a aplicação Streamlit capture os tokens e finalize o processo de redefinição de senha.

## A Solução

Este arquivo `index.html` resolve o problema de forma simples:

1.  Ele é hospedado (por exemplo, no GitHub Pages) e configurado como a URL de redirecionamento no Supabase.
2.  Quando o usuário clica no link do e-mail de redefinição de senha, ele é direcionado para esta página.
3.  O script JavaScript na página captura os tokens do fragmento (`#`).
4.  Ele então reconstrói a URL da aplicação Streamlit, mas desta vez colocando os tokens como parâmetros de busca (`?`).
5.  Finalmente, o script redireciona o usuário para a aplicação Streamlit, que agora consegue ler os tokens e dar continuidade ao fluxo de criação de uma nova senha.

## Como Usar

1.  Faça o upload deste arquivo `index.html` para um serviço de hospedagem estática (como o GitHub Pages).
2.  **Edite o arquivo `index.html`:** Altere a variável `streamlitAppUrl` para a URL da sua aplicação Streamlit.
    ```javascript
    const streamlitAppUrl = "[https://sua-app.streamlit.app/](https://sua-app.streamlit.app/)";
    ```
3.  No seu cliente Supabase, ao chamar a função de envio de e-mail para redefinição de senha, aponte a URL de redirecionamento para onde este `index.html` está hospedado.
