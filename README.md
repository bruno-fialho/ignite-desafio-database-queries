<!-- <p align="right">
  <a href="README.en.md">🇺🇸</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="README.md">🇧🇷</a>&nbsp;&nbsp;&nbsp;
</p> -->

<img alt="Ignite" src=./src/assets/header-ignite.png />

<h2 align="center">
  Desafio 05 - Database Queries
</h2>
<h3 align="center">
  Bootcamp Ignite Node.js 2021 - <a href="https://rocketseat.com.br/">Rocketseat</a>
</h3>

<p align="center">
  <a href="#computer-sobre-a-aplicação">Sobre a aplicação</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#warning-testes">Testes</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#cd-pacotes-instalados">Pacotes instalados</a>&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;
  <a href="#memo-licença">Licença</a>
</p>

## :computer: Sobre a aplicação

Nessa aplicação, são realizadas consultas no banco de dados com o TypeORM de três maneiras:

- Usando o **ORM**
- Usando **Query Builder**
- Usando **Raw Query**

A aplicação possui dois módulos: `users` e `games`. Um **usuário** pode ter vários jogos e um mesmo **jogo** pode estar associado a vários usuários.

### :link: Instruções para clonar repositório

Para rodar a aplicação na sua máquina:

1. `git clone https://github.com/bruno-fialho/ignite-desafio-database-queries`

2. Na pasta do repositório, rodar um `yarn` para instalar as dependências.

3. Para que os testes funcionem, é importante que você crie uma database no banco Postgres com o nome `queries_challenge` e substitua os dados de autenticação no arquivo `ormconfig.json`(`username` e `password`).

### Repositórios da aplicação

#### UsersRepository

- Método **findUserWithGamesById**

  Esse método recebe o **Id** de um usuário e retorna os dados do usuário encontrado juntamente com os dados de todos os **games** que esse usuário possui.

  Aqui é usado o **ORM** para a consulta.

  Exemplo de retorno:

  ```jsx
  {
    id: '81482ac4-29bd-497f-b71a-8ae3b20eca9b',
    first_name: 'John',
    last_name: 'Doe',
    email: 'mail@example.com',
    created_at: '2021-03-19 19:35:09.877037',
    updated_at: '2021-03-19 19:35:09.877037',
    games: [
      {
        id: '63a6c35a-ac97-4773-9021-fb93973c8139',
        title: 'GTA V',
        created_at: '2021-03-19 19:35:09.877037',
        updated_at: '2021-03-19 19:35:09.877037',
      },
      {
        id: '74e4fc3b-434d-4452-94eb-27a85dce8d1a',
        title: 'Among Us',
        created_at: '2021-03-19 19:35:09.877037',
        updated_at: '2021-03-19 19:35:09.877037',
      }
    ]
  }
  ```

- Método **findAllUsersOrderedByFirstName**

  Esse método retorna a listagem de usuários cadastrados em ordem alfabética (**ASC**). 
  
  Aqui é usado **raw query** para a consulta.

- Método **findUserByFullName**

  Esse método recebe `first_name` e `last_name` e retorna um usuário que possua os mesmos `first_name` e `last_name`. Aqui você deve encontrar o usuário ignorando se o argumento passado está em caixa alta ou não. 

  Aqui é usado **raw query** para a consulta.

#### GamesRepository

- Método **findByTitleContaining**

  Esse método recebe parte do título de um jogo ou o título inteiro e retorna um ou mais jogos que derem match com a consulta. 

  Se o método for chamado com o argumento `"or S"` e existir algum jogo com essa sequência de letras no título, o retorno será apresentado conforme esse exemplo:

  ```jsx
  [
    {
      id: '63a6c35a-ac97-4773-9021-fb93973c8139',
      title: 'Need For Speed: Payback',
      created_at: '2021-03-19 19:35:09.877037',
      updated_at: '2021-03-19 19:35:09.877037',
    },
    {
      id: '74e4fc3b-434d-4452-94eb-27a85dce8d1a',
      title: 'Need For Speed: Underground',
      created_at: '2021-03-19 19:35:09.877037',
      updated_at: '2021-03-19 19:35:09.877037',
    }
  ]
  ```

  A consulta também é feita de forma case insensitive, ignorando caixa alta onde no banco não existe. Para exemplo, considerando a busca exemplificada acima, o retorno deve ser o mesmo caso o parâmetro passado seja uma string `"nEEd"`. 

  Aqui é usado **query builder** para a consulta.

- Método **countAllGames**

  Esse método deve retornar uma contagem do total de games existentes no banco.

  Aqui é usado **raw query** para a consulta.

- Método **findUsersByGameId**

  Esse método deve receber o `Id` de um game e retornar uma lista de todos os usuários que possuem o game do `Id` informado. 

  Aqui é usado **query builder** para a consulta.

  Exemplo de retorno:

  ```jsx
  [
    {
      id: '81482ac4-29bd-497f-b71a-8ae3b20eca9b',
      first_name: 'John',
      last_name: 'Doe',
      email: 'mail@example.com',
      created_at: '2021-03-19 19:35:09.877037',
      updated_at: '2021-03-19 19:35:09.877037'
    },
    {
      id: '75920ac4-32ed-497f-b71a-8ae3c19eca9b',
      first_name: 'Usuário',
      last_name: 'Qualquer',
      email: 'usuarioqualquer@example.com',
      created_at: '2021-03-19 19:35:09.877037',
      updated_at: '2021-03-19 19:35:09.877037'
    }
  ]
  ```

## :warning: Testes

Para esse desafio, temos os seguintes testes:

- **[UsersRepository] should be able to find user with games list by user's ID**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é descrito no respectivo método.

- **[UsersRepository] should be able to list users ordered by first name**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é descrito no respectivo método.

- **[UsersRepository] should be able to find user by full name**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é descrito no respectivo método.

- **[GamesRepository] should be able find a game by entire or partial given title**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é descrito no respectivo método.

- **[GamesRepository] should be able to get the total count of games**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é descrito no respectivo método.

- **[GamesRepository] should be able to list users who have given game id**

  Para que esse teste passe, você deve satisfazer o código de acordo com o que é descrito no respectivo método.

## :cd: Pacotes instalados

A seguir segue uma lista dos pacotes instalados:

- [pg](https://github.com/brianc/node-postgres)
- [typeorm](https://github.com/typeorm/typeorm#readme)
- [typescript](https://www.typescriptlang.org/)
- [ts-node](https://github.com/TypeStrong/ts-node)
- [jest](https://jestjs.io/docs/en/getting-started)
- [ts-jest](https://kulshekhar.github.io/ts-jest)
- [supertest](https://www.npmjs.com/package/supertest)

## :memo: Licença

Esse projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.