# Projeto in.orbit

> 💡 **Definição**: Controle de metas pessoais.
> 💡 **Funcionamento**: Ao abrir o aplicativo irá mostrar que não tem nenhuma meta cadastrada.
    Clicando em *Cadastrar Meta* irá mostrar um menu lateral para indicar *Qual atividade/meta* irá querer cumprir e *Quantas vezes na semana* irá querer cumprir.
    Quanto mais vezes selecionar as atividades/metas da semana mais vezes irá precisar cumprir na semana para atingir objetivo de 100%.
    Na sequencia será mostrado uma visualização semanal no topo como 05 a 12 de Agosto, seguido por uma barra de progresso com tantas metas completadas:
    Quando não tiver atividades/metas completadas irá mostrar uma lista que deverá completar, então ao clicar em alguma irá registrar que completou a meta.
    QUando tiver atividades/metas completadas irá mostrar na lista da semana que completou junto com o nome da meta e o horario, então conforme a quantidade de vezes selecionada para cumprir como *Acordar Cedo 2x na semana* e ter cumprir ontem e hoje, irá mostrar o nome da meta visualmente desabilitada não precisando completar mais, com isso, a barra de progresso fica totalmente corelacionada com o *Numero de vezes que tem que completar as metas X Quantas metas ja completou*. 
> 💡 **Foco do Projeto**: 1º - Back-end: SQL.
                          2º - Front-end: - CSS + Dados e Formularios (Como fazer o consumo da API /Conexão do Back-end com o Front-end)

# Construir Front-end

 - Framework: React
 - Ferramenta/Biblioteca: Vite, Biome
 - template: Typescript
 - Biblioteca: Tailwindcss, Radix, TanStack React Query, SWS Vercel
 - Features do projeto:
    - app.tsx -> tela inicial com botão cadastro da meta
              -> menu lateral para abrir formulario de cadastrar meta
              -> tela/pagina principal após o cadastramento do usuário
                 -> cadastrou meta, mas não completou nenhuma meta
                 -> cadastrou meta e ja completou alguma meta

# Conceitos

 - React: Gira em torno de um conceito principal que são os *Componentes*
 - Componete: Forma de separar uma aplicação em varios pedaços que ao juntar forma o projeto
 - Estado: Nada mais é que uma variavel *const*, mas porém, que toda vez que o seu valor for alterado, o valor atualizado dela é refletido em tela.
    - Definição: Um dos conceitos mais importantes do React. A ideia de poder atualizar variaveis e ver esse valor refletido em tela em tempo real.
    - Como criar: chama a variavel *const* de *useState()* passando um valor X retornando um array *[]*, onde a 1º posição é o valor da variavel e a 2º posição é uma função para fazerr a atualização dessa varivel.
    - Variavel: No React quando tem uma variavel que é armazenada no estado, nunca fazer mutação(aumentar ou diminuir) no valor da variavel, mas sim, substituir o valor da variavel, quer dizer, sempre criar um valor novo. Vem do conceito de *Mutabilidade* da *Programação Funcional* principalmente pelo algoritmo que o React usa por baixo dos panos, para detectar mudanças nas variavel e conseguir renderizar de uma maneira mais performatica, mostrar em tela e detectar alterações nas variaveis de uma maneira mais performatica. *Obs: Mais detalhes podem ser encontrados no Artigo da propria documentação do React - Mutabilidade, Algoritmo de Reconciliação*
    - Estrutura que poderia ser usada, mas foi implementado o Estado:
      ```jsx
      let count = 5

      function increment() {
         count += 1
         console.log(count)
      }
      ```
    - Estrutura: 
      ```jsx
      const [count, setCount] = useState(5) //[nomeVariavel, setNomeVariavel] //(Valor)

      //function deve ser implementada dentro do componete, pois as ações que complementam o estado devem estar dentro do componente 
      function increment() {
         setCount(count + 1) //setNomeVariavel e //(NovoValor) = Valor + 1
      }
      ```
 - Chamadas HTTP fetch de dados dentro do React: Pegar/Mostrar resumo do back-end e mostrar em tela, pois, com esses dados conseguir determinar qual componente mostrar.
    - Definição: Após implementar código abaixo, ao acessar o inspecionar na aba *Network* e clicar em *Fetch/XHR* é possivel encontrar a requisição *summary*. *Obs: Caso apareça 2 vezes não se preocupar, pois, é só um comportamento do React.*
       - Essa duplicidade acontece devido a tag <StricMode> no arquivo main.tsx causada no primeiro carregamento da aplicação, mas que é uma tag necessária mesmo que ao comentar ou apagar o execução acontece somente 1 vez, com essa ação o seguinte problema ocorre na execução da aplicação:
          - Se quiser mostrar os dados do \`console.log(data)\`, então sempre que precise alimentar uma informação que vai ser subida em tela usa um *Estado* como \`const [summary, setSummary] = useState(null)\` e no lugar do \`console.log(data)\` usar \`setSummary(data)\` e em tela incluir \`<pre>{JSON.stringify(summary, null, 2)}</pre>\` o null e 2 seria pra identação e deixar o JSON organizado em tela, isso irá trazer em tela o resumo das metas.
          - Código completo de como fica a criação do *Fetch* de dados:
            ```jsx
            const [summary, setSummary] = useState(null)

            fetch('http://localhost:3333/summary').then((response) => {
               return response.jason()
            }).then(data) => {
               setSummary(data)
            }

            return (
               <Dialog>
                  <button type="button" onClick={incrementar}>
                     Incrementar
                  </button>

                  <h1 className="text-4xl">{count}</h1>

                  <pre>
                     {JSON.stringify(summary, null, 2)}
                  </pre>
               </Dialog>
            )
            ```
          - Problema em fazer o *Fetch* de dados dessa forma: No inspecionar da tela na aba *Network* é possivel encontrar a aplicação em loop eterno com o *summary*, comentando a linha \`setSummary(data)\` esse loop para de acontecer. Se o Fetch de dados é feito ou coloque qualquer código na raiz do componete \`console.log('a')\`, o que irá acontecer é, que esse código irá executar toda vez que o componente renderizar, e o que é o componente renderizar, é toda vez que tiver qualquer alteração no estado do componente, então toda vez que clicar no botão *incrementar* a requisição está sendo feita de novo e um novo log é feito de *a* no terminal.
          - O que faz para resolver isso: No *React* tem o *Hook* chamado *useEffect*, o *Hook* são funções que o *React* expóe que começa com *use*, são funções internas, no *useEffect* ele recebe 2 parâmetros, o primeiro é qual função quero executar, por exemplo o *Fetch* de dados, o segundo é quando quero executar e o quando sempre será um *Array* que é chamado de *Array* de dependências, o que acontece é que toda vez que coloca uma variável aqui dentro o *React* entende que sempre que essa variável mudar ele irá executar o *useEffect* de novo, se não, ele nunca mais vai executar.
          - Código completo de como fica a criação do *Fetch* de dados dentro do *useEffect*:
            ```jsx
            useEffect(() => {
               fetch('http://localhost:3333/summary')
                  .then((response) => {
                     return response.json()
               })
               .then(data => {
                  setSummary(data)
               })
            }, [])
            ```

 # Configuração

 - Após criação do Projeto WEB preparar o ambiente instalando as dependencias rodandos os comando: *npm i*
 - Rodar o comando *npm run dev* para receber a URL da aplicação http://localhost:5173/
 - Apagar todos os arquivos e referencias ao *Eslint* devido a utilização do *Biome*
 - Atualizar todo o VSCode usando: no teclado usar o *ctrl + shift + P* e digitar *reload window* e dar enter no *Developer: Reload Window*
 - Realizar mesmas instalações feitas no back-end dos comandos:
    - npm i @biomejs/biome -D
 - Instalação do Tailwindcss acessar o site oficial e seguir o passo a passo no caminho Docs > Documentation > Framework Guides > Vite (Seleciona)
 - Lucide-react (npm i lucide-react) -> Biblioteca de Icones
 - Menos - CSS -> Arquivo zip ui.zip com varios componetes (no react são funções que retornam HTML) para diminuir a contrução do zero do CSS para focar na parte de formulario e conexão do back-end com o front-end
 - Instalação da biblioteca TanStack React Query para Fetch de Dados:
   - npm i @tanstack/react-query
 - Instalação da biblioteca React Hook Form para criação de formulário:
   - npm i react-hook-form @hookform/resolvers zod

# Dicas

# Paleta de Cores

 - Possiblidade de utilizar na documentação do Tailwindcss propriedades do CSS que podem ser usadas, mas na Customization > Colors é possivel usar uma paleta de cores pré estabelecidas podendo ajudar no design e na criatividade: *Zinc*

# Nomenclaturas

 - JSX (Javascript XML) -> HTML: Quando escreve HTML dentro do React se chama JSX
 - ClassName -> Mesmo que Class no JavaScript
 - CamelCase -> No react não são usados *-* para separação de propriedades/atributos, mas sim CamelCase com a primeira letra de cada palavra minúscula e as palavras seguintes iniciando com maiúscula

 # Imagem

 - Carregamento de imagem no React pode ser realizado de 2 formas: 
    - Importação -> import logo from './assets/logo-in-orbit.svg' / <img src={logo} alt="in.orbit"/> *obs: esse tipo de carregamento de imagem via importação, quando é realizado o acesso a página a imagem é carregada no Network do Inspecionar, chamado de carregamneto Lazy - Preguiçoso ocorrendo somente após o usuário ter aberto a aplicação*
    - Vetor -> casos em que a imgem é muito pequena, é possivel utilizar(copiar .svg) o proprio vetor no html separando(colando) em um componente in-orbit-icon.tsx incluindo uma tag <title></tittle>
      - Manipulando .svg -> para manter padronização de nomenclatura CamelCase no React, é possivel transformar o código .svg no site *transform.tools* que disponibiliza uma ferramenta de transformar de varios formatos para outro, no menu *SVG > to JSX* colando o código ajustando para CamelCase

# Testes

 - Nos componentes no caminho *components > ui > dialog.tsx* o <Dialog> pode ser usando para testes incluindo <Dialog open> para deixar sempre aberto

 # Botão

 - Na utilização do <DialogTrigger> e dentro um <Button> analisando no inspecionar é possivel identificar que irá criar um botão dentro de outro devido aos 2 serem um botão, a opção que o Radix oferece a alguns componentes que é incluir <DialogTrigger asChild> para utilizar somente o <Button> de dentro como o botão principal

 # Biblioteca

 - Na realização de Fetch de Dados o React recomenda o uso de biblioteca focada em Fetch de Dados. Existem 2 mais famosas para trabalhar com API HTTP REST e são:
   - TanStack React Query
   - SWS Vercel
   - React Hook Form

# Formulário

- Para trabalhar com formulario no React utilizando validação de senha e funções mais profissionais, a recomendação é o uso de bibliotecas e dentre muitas a mais famosa é a React Hook Form, podendo usar uma biblioteca auxiliar @hookform/resolvers que é a integração do React Hook Form com as bibliotecas de validação zod