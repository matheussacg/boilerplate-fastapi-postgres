# Nome do Sistema


Sistema de exemplo exemplo exemplo


## Backend


## Como começar?

  
1.  **Clonar repositório**: Clone o projeto diarias para sua máquina local.


2.  **Configurar Ambiente Virtual (Opcional para DevOps)**:

- Crie e ative um ambiente virtual:

```bash

python -m venv venv

.\venv\Scripts\activate # Windows

```

3.  **Instalar Dependências**:

- Instale as dependências necessárias:

```bash

pip install -r requirements.txt

```

4.  **Configuração do Ambiente .env**:

- Crie um arquivo `.env` na raiz do projeto e configure as variáveis de ambiente necessárias:

```plaintext

DATABASE_URL=postgresql://user:password@localhost/mydatabase

DB_NOME=Nome do banco

DB_USER=Usuario

DB_SENHA=Senha do banco

DB_HOST=Host

LINK_ACESSO=Link de acesso ao frontend

MAIL_USER=seuemail@email.com

MAIL_FROM=seuemail@email.com

MAIL_PASSWORD=Senha do email

JWT_SECRET=Token de segurança

```

5.  **Criação de Token de Segurança**:

- Para gerar um token de segurança, execute o seguinte comando:

```bash

python -c "import secrets; print(secrets.token_urlsafe(32))"

```

6.  **Banco de Dados e Migrações**:

- Certifique-se de que as variáveis de ambiente relacionadas ao banco de dados estejam configuradas corretamente no arquivo `.env`.

- Verifique as migrações existentes no diretório `alembic/versions` com:

```bash

alembic current

```

- Para aplicar as migrações e atualizar o banco de dados, use:

```bash

alembic upgrade head

```


## Rotas da API - V1

Este diretório contém os endpoints da API para a versão 1.

  


### Estrutura de Diretórios

- `api/v1/endpoints/`
- `funcionario.py`: Endpoint para enviar e-mail de acesso ao sistema.
- `localidades.py`: Endpoint para obter estados e cidades.
- `banco.py`: Endpoint para listar bancos.
- `diaria.py`: Endpoint para cálculos e geração de diárias.

  

### Endpoints funcionario

#### /enviar-link-acesso (http://localhost:8000/api/v1/funcionario/enviar-link-acesso)

Este endpoint envia um link de acesso para o sistema de diárias para o email fornecido.

-   **Método HTTP**: POST
-   **Parâmetros**:
    -   **email**: Endereço de email do destinatário.
-   **Autenticação**:
    -   Não requer autenticação.
-   **Validações**:
    -   Apenas emails com o domínio `@fesfsus.ba.gov.br` são autorizados.
-   **Exemplo de Requisição**:

````bash
curl -X POST -H "Content-Type: application/json" -d '{"email": "usuario@fesfsus.ba.gov.br"}' http://localhost:8000/api/v1/funcionario/enviar-link-acesso

````

**Respostas**:

-   **200 OK**: O email foi enviado com sucesso.

````bash
{
    "message": "Email enviado com sucesso."
}
````

**400 Bad Request**: Quando o email fornecido não está no domínio autorizado.

````bash
{
    "detail": "Apenas emails com o domínio @fesfsus.ba.gov.br são autorizados a receber o link de acesso."
}
````

#   b o i l e r p l a t e - f a s t a p i - p o s t g r e s  
 