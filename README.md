# Projeto - 🛒*Supermercado SQ* 

## Sumário
* [Como começar a usar](#inicio)
* [Arquitetura](#arquitetura)
* [Entidades do Sistema](#entidades)
* [Equipe DevHub](#equipe)


# <a id="inicio"></a> Como começar a usar
## Teste em Nuvem
Primeiro de tudo, certifique-se que na sua máquina você tem instalado as seguintes ferramentas:

- Insomnia: [Link para Download](https://insomnia.rest/download)

A aplicação está hospedada no seguinte link: https://supermercado-sq-backend.herokuapp.com/

Para realizar requisições, você pode tanto realizar direto pelo link, chamando, por exemplo: 
https://supermercado-sq-backend.herokuapp.com/products para trazer todos os produtos cadastrados.

Entretanto a melhor forma de realizar requisições no backend são através do Insomnia.

### Testando através do Insomnia 
Para testar as requisições abra o Insomnia e clique no menu `Application > Preferences`, vá até a guia `Data` e clique em `Import Data`, depois em `From File` e escolha o arquivo [Testes HTTP - Insomnia.json](./Testes%20HTTP%20-%20Insomnia.json) localizado dentro da pasta `/supermercado-SQ/backend`, na dashboard do Insomnia escolha o projeto que foi importado e vá até a guia `DEBUG`, as requisições estão nomeadas e organizadas em pastas ao lado esquerdo com os nomes das tabelas que correspondem.

## Teste Local
Primeiro de tudo, certifique-se que na sua máquina você tem instalado as seguintes ferramentas:

- Git: [Guia de Instalação do Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- Node: [Link para Download](https://nodejs.org/en/download/)
- Insomnia: [Link para Download](https://insomnia.rest/download)

No terminal, clone o repositório do GitHub utilizando o seguinte comando:
```
git clone https://github.com/lucassimoes2407/supermercado-SQ.git
```
Depois rode os seguintes comandos:
```
cd supermercado-SQ
cd backend
```
A partir daí, crie um arquivo chamado .env, e popule ele seguindo o modelo existente no arquivo já existente chamado .env-sample.

Então, execute o comando a seguir para instalar as dependências necessárias do NPM:
```
npm i 
```
Enfim para iniciar o servidor e começar a usar execute :
```
nodemon start 
```
Caso precise reiniciar ou parar o serviço pressione `Ctrl + C` no Terminal.

Para testar as requisições abra o Insomnia e clique no menu `Application > Preferences`, vá até a guia `Data` e clique em `Import Data`, depois em `From File` e escolha o arquivo [Testes HTTP - Insomnia.json](./Testes%20HTTP%20-%20Insomnia.json) localizado dentro da pasta `/supermercado-SQ/backend`, na dashboard do Insomnia escolha o projeto que foi importado e vá até a guia `DEBUG`, as requisições estão nomeadas e organizadas em pastas ao lado esquerdo com os Nomes das tabelas que as Respondem.

***

# <a id="arquitetura"></a> Arquitetura

| Pasta/Arquivo     | Responsabilidade                                                                      |
|-------------------|---------------------------------------------------------------------------------------|
| ./app             | Onde se define a rota de entrada pro endpoint de cada entidade.                       |
| ./src/bin/www     | Principais configurações do servidor.                                                 |
| ./src/config/db   | Principais configurações do banco de dados.                                           |
| ./src/routes      | Responsável por definir as rotas de cada entidade.                                    |
| ./src/controllers | Onde são definidas as regras de negócio, manipulação de dados e verificação de erros. |
| ./src/models      | Responsável por definir as querys SQL de cada entidade do sistema.                    |

***

# <a id="entidades"></a> Entidades do Sistema

## Usuários
#### Regras de negócio
ID|Descrição|
:---:|:---|
RNeg-01| O sistema deve garantir que os dados username e email, de usuário, devem ser únicos 
RNeg-02| O sistema deve garantir que um usuário não seja apagado e sim deixado como inativo
RNeg-03| O sistema deve garantir que ao atualizar os dados de um usuário as regras RNeg-01 e RNeg-02, sejam mantidas

#### Endpoints
| Rota                              | Método | Função                                                       |
|-----------------------------------|--------|--------------------------------------------------------------|
| /users/                           | GET    | Lista todos os usuários                                      |
| /users/username/:username         | GET    | Lista um usuário a partir do username                        |
| /users/id/:id                     | GET    | Lista um usuário a partir do id                              |
| /users/findUsersActive            | GET    | Lista todos os usuários definidos como ativos                |
| /users/findUsersInactive          | GET    | Lista todos os usuários definidos como inativos              |
| /users/                           | POST   | Cria um usuário                                              |
| /users/login                      | POST   | Rota para login                                              |
| /users/logout                     | POST   | Rota para logout                                             |
| /users/setUserActiveAttribute/:id | PUT    | Muda um usuário para ativo ou inativo a partir de um id      |
| /users/:id                        | PUT    | Atualiza um usuário a partir do id   
| /users/:username                  | DELETE | Deleta um usuário a partir do username                       |
| /users/id/:id                     | DELETE | Deleta um usuário a partir do id   

***

## Produtos

#### Regras de negócio
| Id      | Descrição                                                                  |
|---------|----------------------------------------------------------------------------|
| RNeg-01 | Deve ser registrado quem criou qual produto.                               |
| RNeg-02 | Os campos 'Nome' e 'Ingredientes' devem, obrigatoriamente, conter valores. |
| RNeg-03 | Um usuário pode cadastrar até 06 imagens por produto.                      |


#### EndPoints
| Rota                              | Método | Função                                                       |
|-----------------------------------|--------|--------------------------------------------------------------|
| /products/                        | GET    | Lista todos os produtos                                      |
| /products/:productCode            | GET    | Lista um produto a partir do id                              |
| /products/name/:productName       | GET    | Lista produtos com determinado nome                          |
| /products/ingredient/:productIngredient       | GET    | Lista produtos com determinado ingrediente       |
| /products/brand/:productBrand     | GET    | Lista produtos de determinada marca                          |
| /products/                        | POST   | Cria um produto                                              |
| /products/filtered/               | POST   | Filtra produtos com base em nome, e com/sem ingredientes especificos|
| /products/                        | PUT    | Atualiza os dados de um produto                              |
| /products/:productCode            | DELETE | Deleta um produto a partir do id  

***

## Restrições

#### Regras de negócio
ID|Descrição|
:---:|:---|
RNeg-01| O sistema deve permitir o cadastro de dados pelos usuários
RNeg-02| O sistema deve permitir a visualização dos dados cadastrados
RNeg-03| O sistema deve permitir a remoção dos dados cadastrados
RNeg-04| O sistema deve permitir a edição dos dados cadastrados

#### EndPoints
| Rota                              | Método | Função                                                       |
|-----------------------------------|--------|--------------------------------------------------------------|
| /restriction/                     | GET    | Lista todas as restrições                                    |
| /restriction/cod/:cod_restricao   | GET    | Lista uma restição a partir do id                            |
| /restriction/name/                | GET    | Lista uma restrição a partir o seu nome                      |
| /restriction/                     | POST   | Cria uma restrição                                           |
| /restriction/:cod_restricao       | PUT    | Atualiza uma restrição a partir do id                        |
| /restriction/:cod_restricao       | DELETE | Deleta uma restriçãoa partir do id                           |

***

## Usuários X Restrições

#### Regras de negócio
| Id      | Descrição                                                                    |
|---------|------------------------------------------------------------------------------|
| RNeg-01 | Cada entrada na tabela deve conter apenas um cod_usuario e um cod_restricao. |
| RNeg-02 | Podem haver diversas entradas para o mesmo usuário, variando as restrições.  |
| RNeg-03 | Podem haver diversas entradas para uma mesma restrição, variando os usuários.  |

#### EndPoints
| Rota                              | Método | Função                                                       |
|-----------------------------------|--------|--------------------------------------------------------------|
| /user-restriction/:cod_usuario    | GET    | Pega todas as restrições de um usuário                       |
| /user-restriction/:cod_usuario    | POST   | Adicionar uma restrição de um usuário                        |
| /user-restriction/:cod_usuario    | DELETE | Deleta uma restrição de um usuário                           |

***

## Produtos X Restrições

#### Regras de negócio
| Id      | Descrição                                                                    |
|---------|------------------------------------------------------------------------------|
| RNeg-01 | Cada entrada na tabela deve conter apenas um cod_produto e um cod_restricao. |
| RNeg-02 | Podem haver diversas entradas para o mesmo produto, variando as restrições.  |
| RNeg-03 | Pordem haver diversas entradas para a mesma restrição, variando os produtos. |

#### EndPoints
| Rota                              | Método | Função                                                       |
|-----------------------------------|--------|--------------------------------------------------------------|
| /product-restriction/:cod_produto | GET    | Mosta todas as restrições que um produto pode estar inserido |
| /product-restriction/:cod_produto | POST   | Cria uma nova restição associada a um produto                |
| /product-restriction/:cod_produto | DELETE | Apaga uma restrição associada a um produto                   |

***

<div align=center>
<a id="equipe"></a>

| | | | |
|:---|:---|:---|:---|
| <img  src="https://avatars.githubusercontent.com/u/86008336?v=4" width=50px/> | <a href="https://github.com/ismaelzaccah">Ismael Zaccah | <img  src="https://avatars.githubusercontent.com/u/42359787?v=4" width=50px/> | <a href="https://github.com/javelfreitas">Javel Freitas |
| <img  src="https://avatars.githubusercontent.com/u/59093848?v=4" width=50px/> | <a href="https://github.com/wiwiaR">Vitória Ribeiro | <img  src="https://avatars.githubusercontent.com/u/56098754?v=4" width=50px/> | <a href="https://github.com/AglailsonSantiago">Aglailson Santiago |
| <img  src="https://avatars.githubusercontent.com/u/47800237?v=4" width=50px/> | <a href="https://github.com/andreinamendes">Andreina Mendes | <img  src="https://avatars.githubusercontent.com/u/96750112?v=4" width=50px/> | <a href="https://github.com/lucassimoes2407">Lucas Simoes |
| <img  src="https://avatars.githubusercontent.com/u/78513841?v=4" width=50px/> | <a href="https://github.com/BrunoSTB">Bruno Braga | <img  src="https://avatars.githubusercontent.com/u/78852666?v=4" width=50px/> | <a href="https://github.com/Elaine-G-L">Elaine Guedes

 **DevHub ©** Atlântico Academy Bootcamp
 </div>

---
