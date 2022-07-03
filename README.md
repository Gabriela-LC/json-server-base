Markenzie TechPlace – API

Este é o backend da aplicação Markenzie TechPlace, um marketplace para freelancer de TI venderem seus produtos/serviços e pessoas interessadas comprarem! O objetivo dessa aplicação é possibilitar a conexão mais fácil entre desenvolvedores júniores que querem divulgar suas habilidades e conseguir oportunidades de freelancers e pessoas/empresas que necessitam de serviços de desenvolvimento web pontuais.

Endpoints
A API possui 9 endpoints, podendo cadastrar seu perfil, fazer login, cadastrar produtos/serviços, visualizar produtos e suas vendas.
O url base da API é https://markenzie-techplace.herokuapp.com

ROTAS SEM AUTENTICAÇÃO

Criar usuário
POST /register - FORMATO DA REQUISIÇÃO

{
	“email”: ”kenzinho@kenzie..com.br”,
	“password”: “123456”,
	“name”: “Kenzinho da Silva”,
}

FORMATO DE RESPOSTA – 201

{
	"accessToken”: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImdhYmlAbWFpbC5jb20iLCJpYXQiOjE2NTY2NzcyNDcsImV4cCI6MTY1NjY4MDg0Nywic3ViIjoiMiJ9.p3zUjO8qg4abrsKaTQzZ8RFGSYRhfxRNYigVy0plEgo",
	“user”: {
		“email”: “kenzinho@kenzie.com.br”,
		“name”: “Kenzinho da Silva”,
		“id”: 1
		}
}


FORMATO DE RESPOSTA ERRO – 400
Email já cadastrado:

{
	“status”:”error”,
	“message”: “email já existente”
}


Login de usuário

POST /login - FORMATO DA REQUISIÇÃO

{
	“email”: ”kenzinho@kenzie..com.br”,
	“password”: “123456”,
}

FORMATO DE RESPOSTA – 200

{
	"accessToken”: "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImdhYmlAbWFpbC5jb20iLCJpYXQiOjE2NTY2NzcyNDcsImV4cCI6MTY1NjY4MDg0Nywic3ViIjoiMiJ9.p3zUjO8qg4abrsKaTQzZ8RFGSYRhfxRNYigVy0plEgo",
	“user”: {
		“email”: “kenzinho@kenzie.com.br”,
		“name”: “Kenzinho da Silva”,
		“id”: 1
		}
}


FORMATO DE RESPOSTA ERRO – 400

Email/senha não compatíveis:

{
	“status”:”error”,
	“message”: “combinação email e senha não compatíveis”
}



ROTAS COM AUTENTICAÇÃO

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:
Authorization: Bearer {token}
Usuário deve estar logado e ser dono para poder criar, alterar e deletar seus produtos. E todos os usuários logados podem ver os produtos.


Listar produtos
GET /products - FORMATO DA RESPOSTA - 200
[
    {
        “name”: ”LandingPage”,
        “price”: 350,
        “description”:”Crio uma nova Landing Page para o seu produto a partir de um design já definido...”,
        “id”:1,
        “userId”:1
    },
    {
        “name”: ”Gerenciador financeiro”,
        “price”: 350,
        “description”:”Crio um Gerenciador financeiro a partir de um design já definido...”,
        “id”:2,
        “userId”:1
}
]




Acessar produto específico
GET /products/:product_id - FORMATO DA RESPOSTA - 200

{
	“name”: ”LandingPage”,
	“price”: 350,
	“description”:”Crio uma nova Landing Page para o seu produto a partir de um design já definido...”,
	“id”:1,
	“userId”:1
}


Criar produtos
POST /products - FORMATO DA REQUISIÇÃO

{
	“name”: ”LandingPage”,
	“price”: 350,
	“description”:”Crio uma nova Landing Page para o seu produto a partir de um design já definido...”,
	“id”:1,
	“userId”:1
}


FORMATO DA RESPOSTA ERRO - STATUS 400
Não preencheu algum campo:

{
	“status”:”error”,
	“message”: [
        “campo description é obrigatório”, 
        “campo price é obrigatório”
        ]
}


Modificar de produto
PUT /products/:product_id - FORMATO DA REQUISIÇÃO

{
	“price”: 300
}


Deletar produto
DELETE / products/: product_id
Não é necessário corpo para a requisição


Listar vendas
Quando uma venda é confirmada e criada pelo sistema apenas o dono da venda pode ler
GET /sales - FORMATO DA RESPOSTA – 200

[
    { 
    “product”: {
        “name”: ”LandingPage”,
        “price”: 350,
        “description”:”Crio uma nova Landing Page para o seu produto a partir de um design já definido...”,
        “id”:1,
        “userId”:1
        }

    “buyedId”: 5,
    “paymentMethod”: “Cartão de crédito”
    “date”: “24/08/2021”,
    “saleId”: 324
    },
    {
    “product”: {
        “name”: ”LandingPage”,
        “price”: 350,
        “description”:”Crio uma nova Landing Page para o seu produto a partir de um design já definido...”,
        “id”:1,
        “userId”:1
        }
    “buyedId”: 23,
    “paymentMethod”: “PIX”
    “date”: “11/06/2021”
    “saleId”: 190
    },
    {
    “product”: {
        “name”: ”Gerenciador financeiro”,
        “price”: 350,
        “description”:”Crio um Gerenciador financeiro a partir de um design já definido...”,
        “id”:2,
        “userId”:1,
        }
    “buyedId”: 3,
    “paymentMethod”: “Boleto”
    “date”: “10/10/2021”,
    “saleId”: 60
}
]
Acessar venda específica

GET /sales/:sale_id - FORMATO DA RESPOSTA - STATUS 200

{
    “product”: {
        “name”: ”LandingPage”,
        “price”: 350,
        “description”:”Crio uma nova Landing Page para o seu produto a partir de um design já definido...”,
        “id”:1,
        “userId”:1
    }

“buyedId”: 23,
“paymentMethod”: “PIX”
“date”: “11/06/2021”
“saleId”: 190
}
