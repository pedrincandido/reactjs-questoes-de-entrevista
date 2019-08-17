# React Entrevista Questões & Respostas

Se você gostou desse projeto, faça um Pull Request será de muita ajuda :].

### Table of Contents

| No. | Questões |
| --- | --------- |
|   | **Core React** |
|1  | [O que é React?](#o-que-é-react) |
|2  | [Quais são os principais recursos do React?](#quais-são-os-principais-recursos-do-react) |
|3  | [O que é JSX?](#o-que-é-jsx) |
|4  | [Qual a diferença entre um Elemento e um Component?](#qual-a-diferença-entre-um-elemento-e-um-component) |
|5  | [Como criar um component em React?](#como-criar-um-component-em-react) |
|6  | [Quando usar um component de classe e um component de função?](#quando-usar-um-component-de-classe-e-um-component-de-função) |
|7  | [ O que são components puros?](#o-que-são-components-puros) |
|8  | [Qual a diferença entre um component e um PureComponent?](#qual-a-diferença-entre-um-component-e-um-purecomponent) |
|9 | [Quando usar um PureComponent?](#quando-usar-um-purecomponent) |
|10 | [O que é estado em React?](#o-que-é-estado-em-react) |
|11 | [O que é props in React?](#o-que-é-props-in-react) |
|12 | [Qual a diferença entre estado e props?](#qual-a-diferença-entre-estado-e-props) |
|13 | [Por que não devemos atualizar o estado diretamente?](#por-que-não-devemos-atualizar-o-estado-diretamente) |
|14 | [Qual é o proposito da função callback como um argumento de setState()?](#qual-é-o-proposito-da-função-callback-como-um-argumento-de-setstate) |
|15 | [Qual a diferença entre tratamento de eventos em HTML e React?](#qual-a-diferença-entre-tratamento-de-eventos-em-html-e-react) |
|15 | [Como ligar o metodo ou event handlers em JSX callbacks?](#como-liga-o-metodo-ou-event-handlers-em-jsx-callbacks) |


## Core React

1. ### O que é React?

    React é uma **biblioteca frontend JavaScript open-source** que é usada para construir ui especialmente para SPA(single page applications). É usada para manipulação da camada de visualização para web e aplicativos mobiles. React foi criado por Jordan Walke, um software engineer trabalhando para o Facebook. O  React foi implementado pela primeira vez no Feed do Facebook's em 2011 e no Instagram em 2012.
    
2. ### Quais são os principais recursos do React?
    
    Os principais recursos do react são:
    
    * Usa o **VirtualDOM** em vez de RealDOM, considerando as manipulações do RealDOM caras.
    * Suporte **server-side rendering**.
    * Seguidores **Unidirecional** fluxo de dados ou data binding.
    * Usa **reusable/composable** UI de componentes para desenvolvimento da view.
    
3. ### O que é JSX?

    ```jsx harmony
    const element = <h1>Hello, world!</h1>;
    ```

    Esta sintaxe estranha de tags não é uma string, nem HTML, é chamada *JSX* uma extensão de sintaxe do ECMAScript (o acrônimo significa *JavaScript XML*). Basicamente ele nós da expressividade de JavaScript junto com o HTML como sintaxe de template. O exemplo abaixo pode lembrar uma linguagem de template, mas vem com todo o poder do JavaScript. Lembrando que o JSX não é obrigatório para utilizar o React.
    
    Neste exemplo o texto dentro da tag `<h1>` retorna como uma função Javascript para a função render.
    
    ```jsx harmony
    class App extends React.Component {
      render() {
        return(
          <div>
            <h1>{'Bem vindo ao mundo reativo!!'}</h1>
          </div>
        )
      }
    }
    ```

4. ### Qual a diferença entre um Elemento e um Component?
    Um *Elemento* é um objeto simples que descreve o que você quer que apareça na tela. Criar um elemento é barato, um elemento pode conter outros elementos, e umma vez que o elemento é criado, ele nunca é alterado.
    
    A representação de um React Element objeto seria a seguinte: 
    
    ```javascript
    const element = React.createElement(
    'div',
    {id: 'login-btn'},
    'Login'
    )
    ```
    O exemplo acima a função `React.createElement()` retorna um objeto: 
    
    ```
    {
        type: 'div',
        props: {
            children: 'Login',
            id: 'login-btn'
        }
    }
    ```
    
    E finalmente para renderizar no DOM usa `ReactDOM.render()`:
    
    ```html
    <div id='login-btn'>Login</div>
    ```
    
    Enquanto que um **componente** pode ser declaro de várias manerias diferentes. Podendo ser uma classe com um método `render()`. Em um simples caso, uma outra alternativa, você pode definir uma função. Em qualquer um dos casos, ele usa props como entrada e retorna um JSX como saída:
    
     ```javascript
    const Button = ({ onLogin }) =>
      <div id={'login-btn'} onClick={onLogin}>Login</div>
    ```
    
    Então o JSX transpila a função `React.createElement()` a saída:
    
    ```javascript
    const Button = ({ onLogin }) => React.createElement(
      'div',
      { id: 'login-btn', onClick: onLogin },
      'Login'
    )
    ```
    
5. ### Como criar um component em React?

    Existe duas maneiras possíveis para criar um component.
    
    1. **Function Components:** Isto é um jeito simples de criar um component. Essas são funções puras de JavaScript ela aceita props objetos como seu primeiro parâmetro e retorna React elementos:
    
        ```jsx harmony
        function Greeting({ message }) {
            return <h1>{`Olá, ${message}`}</h1>
        }
        ```
    2. **Class Components:** Além disso você pode usar classes do ES6 para definir seu component. Uma função component pode ser escrita assim:
     
        ```jsx harmony
        class Greeting extends React.Component {
           render() {
             return <h1>{`Olá, ${this.props.message}`}</h1>
           }
        }
        ```

6. ### Quando usar um component de classe e um component de função?

    Se o seu component precisar de um estado ou de um ciclo de vida então use component class, de outra forma use a component função.

7. ### O que são components puros?

     É uma das maneiras mais significativas de otimizar os aplicativos React. O uso de pure component fornece um aumento considerável no desempenho pois reduz o número de operações de renderização no aplicativo. *`React.PureComponent`* é exatamente o mesmo de *`React.Component` exceto pelo fato de lidar com o `shouldComponentUpdate()` para você. Nós sempre devemos tentar fazer o nosso estado o mais simples póssivel, minimizando o número de estados do component.

8. ### Qual a diferença entre um component e um PureComponent?
      A principal diferença entre um Component e um PureComponent é que o PureComponent modifica a forma em que o diff é feito no processo de renderização, basicamente, a verificação de dados pro update do componente é feita no modo shallow.

      ![pure](images/pure.gif)

      Isto significa que: Em uma comparação de não-objetos (array, primitive, type, etc) o conteúdo é que é utilizado como item para comparação enquanto que, quando você compara objetos, apenas a referência é verificada.

      Principalmente por conta dessa shallow comparison é o que uso de PureComponent pode incrementar a perfomance da sua aplicação na renderização de components.

9. ### Quando usar um PureComponent?
      1. State/Props devem ser imutáveis
      2. State/Props não devem ter uma hierarquia
      3. Você deve controlar quando o dado muda através de forceUpdate()
         ou dispatch de actions
      4. Os filhos desse component devem ser puros

10. ### O que é estado em React?

      *Estado* do component é um objeto que segura algumas informações que pode mudar ao longo do ciclo de vida de um component. Devemos sempre tentar fazer nosso estado o mais simples possível e minimizar o numero de component com estado. Agora vamos criar um user component com uma message de estado

      ```jsx harmony
      class User extends React.Component {
        constructor(props) {
          super(props)

          this.state = {
            message: 'Bem vindo ao mundo Reativo!!'
          }
        }

        render() {
          return (
            <div>
              <h1>{this.state.message}</h1>
            </div>
          )
        }
      }
      ```

      ![state](images/state.jpg)

      Estado é similar a props, mas ele é privado e totalmente controlado pelo component. i.e, não é acessível a nenhum component que não seja o que o possui e o define. 
  
11. ### O que é props in React?

    *Props* são a entrada para component. Eles são valores únicos ou objetos que contêm um conjunto de valores que são transmitidos aos components na criação usando uma convenção de nomenclatura semelhante aos atributos de HTML-tag. Eles são dados passados de um component pai para um component filho.

    O primeiro próposito de uma props no React é para fornecer a seguinte funcionalidade ao component:
    1. Passar custom data para o seu component.
    2. Desencadear mudanças no estado.
    3. usar atráves da `this.props.reactProp` dentro do component's `render()` método.

    Para este exemplo, vamos criar um elemento com `reactProp` propriedade: 

    ```jsx harmony
    <Element reactProp={'1'} />
    ```

    Este `reactProp` nome (ou qualquer coisa que você criou) torna-se uma propriedade anexada ao objeto props nativo do react que originalmente já existe em todos os componets criado usando a biblioteca React.

    ```
    props.reactProp
    ```

12. ### Qual a diferença entre estado e props?

    Ambos *props* e *estado* são objetos simples em JavaScript. Enquanto ambos possuem informações que influenciam a saída e renderização, eles são diferentes nas funcionalidades com respeito ao component. Props são passados para o component semelhante aos parâmetros passados em funções, enquanto que o estado é gerenciado com o componente semelhante as variavéis declaradas em funções.

13. ### Por que não devemos atualizar o estado diretamente?

    Se você tentar atualizar o estado diretamente então não vai  re-renderizar o component. 

    ```javascript
    ///Errado
    this.state.message = 'Olá mundo!'
    ```

    Em vez disso, use o método `setState()`. Ele agenda uma atualização para o objeto de estado de um component. Quando o estado muda, o component responde por fazer uma renderização.

    ```javascript
    //Correto
    this.setState({ message: 'Olá mundo!!' })
    ```
    
    **Nota:** Você pode atribuir diretamente ao objeto de estado em um *construtor* ou usando a sintaxe de declaração de campo de classe javascript mais recente.

14. ### Qual é o proposito da função callback como um argumento de `setState()`?

    A função callback(retorno de função) é invocada quando o setState é concluído e o component é renderizado. Como a função `setState()` é **assíncrona** o callback(retorno de função) é usada para continuar a execução do código após uma operação **assíncrona** terminar. 

    **Nota** É recomendado usar o método de ciclo de vida em vez de função callback.

    ```javascript
    setState({ name: 'Pedro' }, () => console.log('O nome é atualizado e o componente re-renderizado'))
    ```

15. ### Qual a diferença entre tratamento de eventos em HTML e React?
    
    1. No HTML o evento deve ser declarado em *lowercase*:

    ```html
    <button onclick='activateLasers()'>
    ```

    Enquanto no React o mesmo é usando a convenção *camelCase*:

    ```jsx harmony
    <button onClick={activateLasers}>
    ```

    2. No HTML você pode retornar `false` para prevenir o prevent default:

    ```html
    <a href='#' onclick='console.log("Este link foi clicado."); return false;' />
    ```

    Enquanto isso no React você deve chamar o `preventDefault()` explicitamente:

    ```javascript
    function handleClick(event) {
      event.preventDefault()
      console.log('Este link foi clicado.')
    }
    ```

16. ### Como ligar o metodo ou event handlers em JSX callbacks?

    Você tem 3 possiveis maneiras de fazer isso:

    Com createReactClass(), isso não é necessário por que ele faz bind de todos os métodos, sem ES6.

    1. **Ligar no construtor:** Em JavaScript classes ES6, os métodos seguem a mesma semântica que classes E6S regulares, não estão vinculados por padrão. Isso significa que elas não fazem o bind do ``this`` da istância. Você terá que explicitamente usar ``.bind(this)``. A mesma coisa aplica-se para os event handlers no React definido como as classes métodos. Normalmente devemos ligar o construtor.

    ```javascript
    class Component extends React.Componenet {
      constructor(props) {
        super(props)
        this.handleClick = this.handleClick.bind(this)
      }

      handleClick() {
        // ...
      }
    }
    ```

    2.  **Public class fields syntax** Se você não gosta de usar a abordagem bind no constructor então **public class fields syntax** pode ser usado para vincular callbacks(retornos de chamadas) corretamente.

     ``AVISO: essa sintaxe é experimental!``
      ``Usar uma arrow function aqui já faz bind do método``
    ```jsx harmony
    handleClick = () => {
      console.log('isto é:', this)
    }
    ```
     **Nota:**: A sintaxe acima é ``experimental`` que a sintaxe pode mudar.

    ```jsx harmony
    <button onClick={this.handleClick}>
      {'Click me'}
    </button>
    ```

    3. **Arrow functions em callbacks(retorno de chamadas):** Você pode usar *arrow functions* diretamente em callbacks(retornos de chamadas).
    
    ```jsx harmony
    <button onClick={(event) => this.handleClick(event)}>
      {'Click me'}
    </button>
    ```

    **Nota:** Se o callback(retorno de chamada) é passado como propriedade para o component filho, esse component pode fazer um extra renderização. Nesses casos, é preferível usar a abordagem `.bind()` ou **public class fields syntax**, considerando a performance e o desempenho.