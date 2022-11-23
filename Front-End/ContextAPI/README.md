# Checklist-Context

*Antes de começar, atenção as regras dos hooks:*
https://pt-br.reactjs.org/docs/hooks-rules.html

*Dentro da pasta `src`:*

- [ ] Criar uma pasta `context`;
- [ ] Dentro da pasta `context` vamos criar um arquivo `myContext.js`;

*Dentro do arquivo `myContext.js`:*

- [ ] Importar do react o `createContext`;
- [ ] Criar uma variável `context` que vai receber o resultado do `createContext()`;
- [ ] Exportar a nossa variável;

Exemplo:

```js
import { createContext } from 'react';

const context = createContext();

export default context;
```

### Criando o `Provider`

Lembrando que o Provider é um componente que vai conter nossos estados globais da aplicação, geralmente importamos ele no `index.js` que é o ponto mais alto da hierarquia de componentes para prover nossos estados para todos os seus filhos.

- [ ] Dentro da pasta `context` vamos criar um arquivo `myProvider.js`;
- [ ] Vamos importar nosso `MyContext` nesse arquivo e criar o componente `Provider`;
- [ ] Recebemos via props os `children` da árvore de componentes;
- [ ] No retorno do Provider vamos chamar via tag o nosso `MyContext.Provider` que recebe um `value` como prop;
- [ ] Passamos dentro da tag os nossos `children` que serão alimentados pelo `value` do Provider;

OBS: A construção dos estados dentro do Provider depende do componente ser funcional ou de classe:
 - Para classes utilizamos o `this.state`;
 - Para funções utilizamos hooks, `useState`;

```js
// EXEMPLO COM COMPONENTE FUNCIONAL

import React, { useState } from 'react';
import MyContext from './MyContext';

const INITIAL_STATE = { nome: 'Xablau', idade: 100 };

function Provider({ children }) {
  const [state, setState] = useState(INITIAL_STATE);

  return (
    <MyContext.Provider value={ state }>
      {children}
    </MyContext.Provider>
  )
}

export default Provider;
```

```js
// EXEMPLO COM COMPONENTE CLASSE

import React, { useState } from 'react';
import MyContext from './MyContext';

const INITIAL_STATE = { nome: 'Xablau', idade: 100 };

class Provider extends React.Component {
  state = INITIAL_STATE;

  render() {
    const { children } = this.props;
  
    return (
      <MyContext.Provider value={ { ...this.state } }>
        {children}
      </MyContext.Provider>
    )
  }
}

export default Provider;
```

### No arquivo `index.js`
- [ ] Vamos importar o nosso componente `Provider` englobando nosso app;

```js
import Provider from './context/MyProvider'

<Provider>
   <App />
</Provider>
```

Agora toda nossa aplicação está sendo alimentada pelos dados disponibilizados no value do nosso Provider.
Por fim só precisamos resgatar esses dados em qualquer componente da nossa aplicação.

OBS: Para consumir os dados também vai depender do componente ser funcional ou classe:
 - Para classes utilizamos o `MyContext.Consumer` ou podemos utilizar o `contextType`;

```js
 // EXEMPLO MyContext.Consumer

<MyContext.Consumer>
  {(value) => { // recebe o value provido pelo Contexto
    /* renderiza algo utilizando o valor recebido do contexto */
  }}
</MyContext.Consumer>
```

```js
// EXEMPLO contextType
import MyContext from './context/MyContext';

const value = this.context // recebe o value provido pelo Contexto

MyComponent.contextType = MyContext; // Criar fora da classe
```

 - Para funções utilizamos hooks, `useContext`;

```js
// EXEMPLO COM HOOK useContext

import React, { useContext } from 'react';
import MyContext from './context/MyContext';

const value = useContext(MyContext); // recebe o value provido pelo Contexto
```

