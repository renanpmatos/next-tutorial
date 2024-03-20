### Next.js é um framework completo Full-Stack baseado em [[React.js]]

### Comparação React.js X Next.js 🆚

#### [[React.js]] :

- Não consegue criar uma aplicação completa pronta para produção.
- React é uma biblioteca para criar User Interfaces (Camada View)
- É preciso decidir sobre outras features como routing, data fetching etc.

#### Next.js :

- É um framework completo baseado em React.js para construir User Interfaces
- Apresenta outras features para construir aplicações prontas para produção.
- Estas features incluem routing, data fetching, bundling, compiling etc
- Não é necessário instalar pacotes adicionais, pois o Next já possuí tudo que é necessário
- Possuí Opiniões e Conveniências que devem ser seguidas para implementar as features

### Primeiros Passos 🚶

#### Principais Features do Next.js:

1.  Routing
2.  API Routes
3.  Rendering (Server Side e Client Rendering)
4.  Data Fetching
5.  Styling
6.  Optimization
7.  Dev and Prod build system

#### Requisitos para rodar Next.js: [[Node.js]]

#### Criando uma aplicação:

Este comando deve ser executado no terminal, utilizando um gerenciador de pacotes node, como o **npm** neste caso. Criará uma aplicação nova depois de configurar o projeto pelo próprio terminal.

```shell
npx create-next-app@latest
```

#### Executando uma aplicação:

O comando irá iniciar um servidor localhost na porta 3000 por padrão, sendo assim um ambiente de desenvolvimentos

```shell
npm run dev
```

#### Instalando pacotes em uma aplicação:

Caso tenha baixado um projeto next ou clonado um repositório, será necessário instalar as bibliotecas e dependências. Para isso utilize o seguinte comando:

```shell
# vai instalar todos os pacotes presentes no package.json
npm install

# vai instalar um pacote específico
npm install nome-do-pacote
```

### Estrutura do Projeto Next.js: 📂

Logo após criar uma aplicação nova e executando pela primeira vez, podemos observar a seguinte estrutura de projeto:

<img src="https://github.com/renanpmatos/regex-ninja/blob/main/public/tutorial-images/Pasted image 20240306134219.png">

#### Pastas:

1.  **.next** -> É criada quando rodamos scripts _dev_ ou _build_, sendo a partir dela que a aplicação é carregada num servidor próprio.

2.  **node_modules** -> É aqui que as dependências do projeto são instaladas, sendo gerada ao rodar o comando `npm install`.

3.  **public** -> Onde são localizadas as imagens e assets da aplicação

4.  **src** -> É a pasta **mais importante**, pois contêm os reais arquivos de trabalho. Contêm a pasta app do projeto.

#### Pasta app:

Esta pasta contempla o sistema de rotas do Next, conhecido como App Router e contêm os seguintes arquivos:

1.  **favicon.ico** -> Logo da vercel que aparece no navegador ao lado do nome da pagina

2.  **globals.css** -> É o CSS global do projeto

3.  **layout.tsx** -> A UI que pode ser compartilhada entre diferentes páginas da aplicação. contêm as configurações iniciais de HTML, então mesmo que tenha sido deletado, ao executar o projeto é criado novamente.

4.  **page.tsx** -> É o componente principal (home) carregado na rota padrão `localhost:3000/`. Este componente substituí a props `children` do layout.tsx para formar a UI completa que vemos no navegador

#### Demais Arquivos:

1. **package.json**
   É um arquivo JSON que contêm as dependências do projetos, scripts e pacotes necessários para execução. É neste arquivo que se configura os comandos para executar uma aplicação.

   ![[Pasted image 20240306132726.png]]

2. **next.config.mjs** -> configuração do nextjs no ambiente
3. **tsconfig.json** -> configuaração do Typescript no projeto
4. **next-env.d.ts** -> configuração do Typescript exclusiva para o ambiente Next
5. **tailwind.config.ts** -> configuração do TailwindCSS no projeto
6. **postcss.config.js** -> configuração para o CSS do Tailwind
7. **.gitignore** -> arquivo para definir as dependências que deverão ser ignoradas no processo de commit ao [[Git]]
8. **.eslintrc.json** -> configuração do EsLint para o projeto

### Entendendo os Componentes 🧩

Desde a versão 18 do React, foi introduzido uma feature chamada React Server Components, que trouxe uma nova maneira de se criar componentes para as páginas do projeto.

O Next.js passou a adotar essa mesma arquitetura de construção de componentes, dividindo-os em duas categorias:

- **Server Components**
  - No Next.js, todos os componentes são server components por padrão
  - Conseguem executar tarefas no lado do servidor, antes do componente ser retornado para o cliente, podendo ler arquivos, data fetching de um banco de dados etc.
  - **Não** conseguem usar hooks ou lidar com as interações de usuário, justamente por ser pré-renderizados no servidor
- **Client Components**
  - Para definir um client component, é necessário adicionar `"use client"` no topo do arquivo do componente.
  - **Não** conseguem executar tarefas como ler arquivos, mas podem usar hooks e administrar as interações do usuário.

### Sistema de Rotas 🗺️

#### App Router System:

O sistema de roteamento do Next.js é baseado nos próprios arquivos do projeto, onde as URLs que os usuários acessam no navegador são definidos por arquivos e pastas na estrutura de código.

#### Regras ⚠️

- Todas as rotas devem ser colocadas na pasta **app**
- Todo arquivo correspondente a uma rota deve ser nomeado de **page.tsx** ou **page.js**
- Toda pasta corresponde a um segmento na URL no navegador

Então mesmo que uma rota exista, ela não será carregada a menos que siga todas as regras:
![[Pasted image 20240306200926.png]]![[Pasted image 20240306200949.png]]![[Pasted image 20240306200936.png]]
A pagina não foi encontrada pois não há um arquivo **page.tsx**, embora um componente tenha sido exportado

#### Exemplo 1 (Simple Routes):

Ao criar uma rota _about_ no projeto, fazemos as seguintes modificações:

Adicionamos uma pasta **about** com um arquivo **page.tsx** contendo um componente simples
![[Pasted image 20240306161200.png]] ![[Pasted image 20240306161356.png]]
Assim, ao acessar a rota, o componente é carregado
![[Pasted image 20240306161527.png]]

#### Exemplo 2 (Nested Routes):

Agora criaremos uma rota _blog_ que contenha duas **sub rotas**: _/blog/first_ e _/blog/second_
Neste caso a estrutura é semelhante ao exemplo anterior:

Criamos uma pasta _blog_, com duas pastas dentro, _first_ e _second_, lembrando de colocar arquivos **page.tsx** para carregar os componentes.
![[Pasted image 20240306163145.png]]
![[Pasted image 20240306163426.png]] -> note que aqui acessamos a rota **/blog**
![[Pasted image 20240306163431.png]] -> rota **/blog/first**![[Pasted image 20240306163434.png]] -> rota **/blog/second**

#### Exemplo 3 (Dynamic Routes):

Neste exemplo criaremos uma rota _products_, que tem uma **sub rota** dinâmica que receba o _id_ de um produto e retorne uma página com os detalhes daquele produto.

Primeiramente criamos a rota _products_, com um arquivo **page.tsx**:
![[Pasted image 20240306171306.png]]
![[Pasted image 20240306171216.png]]

Para definir uma Rota Dinâmica, criamos uma pasta com o nome `[productId]`, dessa forma dizemos que o parâmetro da rota varia, mas é associado à variável **productId**. Criamos também um componente **page.tsx** para que deve receber como parâmetro um objeto que será associado à **productId**

![[Pasted image 20240306172004.png]] ![[Pasted image 20240306172015.png]]
No parâmetro do componente recebemos um objeto _param_ que foi desestruturado para ser associado ao **productId**.

Assim ao Executar, temos as seguintes respostas:
![[Pasted image 20240306172215.png]] -> Rota _/products_![[Pasted image 20240306172234.png]] -> Rota dinâmica de`[productId]`

#### Exemplo 4 (Nested Dynamic Routes):

Agora imagine que queremos acessar as reviews de um produto por uma rota dinâmica, como em:
`localhost:3000/products/1/reviews/1`

Seguiremos as mesmas lógicas dos exemplos anteriores, criando uma rotas **reviews** com uma rota dinâmica `[reviewId]` que terá um componente **page.tsx**:
![[Pasted image 20240306174943.png]]![[Pasted image 20240306175017.png]]
No componente, recebemos também um objeto _params_ que foi desestruturado para receber tanto o **productId** quanto o **reviewId**.

Assim temos na execução:
![[Pasted image 20240306175307.png]]

#### Exemplo 5 (Catch-all Segments):

Imagine um cenário onde temos um rota de **docs** que possuí várias **features** e que cada feature possuí vários **Concepts**, como representado na imagem abaixo:
![[Pasted image 20240306183153.png]]
Diferentemente dos outros exemplos, nesse caso a rota precisa ser completamente variável, podendo obter qualquer tipo de comportamento como:

`localhost:3000/docs/features`
`localhost:3000/docs/concepts/exemplos/ex2`
`localhost:3000/docs/etc`

Primeiramente criamos uma rota simples **docs** e em seguida passamos criamos outra rota, porém está será completamente dinâmica, não obedecendo a um padrão:
![[Pasted image 20240306184247.png]]
Observe que o nome da pasta é `[...slug]`, semelhante à uma Dynamic Route, porém estes `...` definem que não seguirá nenhum padrão, pegando todos os seguimentos de rotas e sempre retornando o **page.tsx**

![[Pasted image 20240306192409.png]]
Ao desestruturar o objeto _params_, vemos que ele se comporta como um **Array de Strings**. Dessa forma, podemos manipular possíveis rotas como se tivéssemos operando um Array.
Obtemos então, o seguinte comportamento:
![[Pasted image 20240306193124.png]]![[Pasted image 20240306193152.png]]

---

Caso queira deixar a rota `[...slug]` como opcional e retornar sempre o **page.tsx**,
basta fazer as seguintes alterações:

1. mude o nome da pasta para -> `[[...slug]]`
2. onde tiver `params.slug`, deixe como opcional -> **params.slug?**

Ficando assim:
![[Pasted image 20240306194126.png]]

#### Customizando a Not-Found Page

Quando tentamos acessar uma rota que não existe, temos uma mensagem de erro de página não encontrada. Porém esta é uma mensagem padrão do Next.js e podemos customizar à vontade

Para isso precisamos criar um arquivo dentro de **app**, chamado de **not-found.tsx**
Este arquivo pode ser completamente personalizado, como no exemplo abaixo:
![[Pasted image 20240306195232.png]]

Podemos inclusive personalizar uma página not-found para uma rota específica, criando este mesmo arquivo dentro da pasta da rota. Além disso, podemos manipular este componente usando a biblioteca `next/navigation`:

Exemplo:
![[Pasted image 20240306195856.png]]

#### Pastas Privadas

Uma **pasta privada** indica que é uma implementação exclusiva e não deve ser considerada pelo sistema de rotas.

Dessa forma, a pasta e todas as **sub pastas** serão excluídas do roteamento, podendo ser utilizadas para melhor organização do código e lógica.

Para definir uma **pasta privada** apenas coloque um `_` no inicio do nome:
Ex: `_lib`
