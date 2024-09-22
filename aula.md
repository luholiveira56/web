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
 - Biblioteca: Tailwindcss, Radix
 - Features do projeto:
    - app.tsx -> tela inicial com botão cadastro da meta
              -> menu lateral para abrir formulario de cadastrar meta
              -> tela/pagina principal após o cadastramento do usuário
                 -> cadastrou meta, mas não completou nenhuma meta
                 -> cadastrou meta e ja completou alguma meta

# Conceitos

 - React: Gira em torno de um conceito principal que são os *Componentes*
 - Componete: Forma de separar uma aplicação em varios pedaços que ao juntar forma o projeto

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