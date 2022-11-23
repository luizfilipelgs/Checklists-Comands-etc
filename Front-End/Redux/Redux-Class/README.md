# Criando um projeto com React e Redux

#### *Antes de começar*
- [ ] pensar como será o *formato* do seu estado global
- [ ] pensar quais actions serão necessárias na sua aplicação

#### *Instalação*
- [ ] npx create-react-app my-app-redux;
- [ ] npm install --save redux react-redux;
- [ ] npm install --save redux-devtools-extension

#### *Criar dentro do diretório `src`:*
- [ ] diretório `redux`

#### *Criar dentro do diretório `redux`*
- [ ] diretório `store`
- [ ] diretório `actions`
- [ ] diretório `reducers`

#### *Criar dentro do diretório `store`:*
- [ ] arquivo `index.js`.

#### *Criar dentro do diretório `actions`:*
- [ ] arquivo `index.js`.

#### *Criar dentro do diretório `reducers`:*
- [ ] arquivo `index.js`.

#### *Criar dentro do arquivo `redux/store/index.js`:*
- [ ] importar o createStore
- [ ] configurar o [Redux DevTools](https://github.com/reduxjs/redux-devtools)
- [ ] importar o rootReducer
- [ ] criar e exportar a store

Exemplo:

```js
import { createStore } from 'redux';
import { composeWithDevTools } from '@redux-devtools/extension'; // Ou 'redux-devtools-extension';
import rootReducer from '../reducers';

const store = createStore(rootReducer, composeWithDevTools());

export default store;
```

Quando necessario thunk:

```js
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevTools } from '@redux-devtools/extension'; // Ou 'redux-devtools-extension';
import thunk from 'redux-thunk';
import rootReducer from '../reducers';

const store = createStore(
  rootReducer,
  composeWithDevTools(
    applyMiddleware(thunk),
  ),
);

export default store;
```

#### *No arquivo `index.js` em `src/index.js` :*
- [ ] importar a `store`
- [ ] importar o `Provider`, para fornecer os estados a todos os componentes encapsulados pelo `<App />`

Exemplo:

```js
// Na importação
import { Provider } from 'react-redux';
import store from './redux/store';
```

```js
// No render
 <Provider store={ store } >
   <App />
 </Provider>
```

#### *Na pasta `actions/index.js`:*
- [ ] criar e exportar os actionTypes

Exemplo:

```js
// ACTIONS TYPES
export const SAVE_EMAIL = 'SAVE_EMAIL';
```

- [ ] criar e export os actions creators necessários

Exemplo:

```js
// ACTIONS CREATORS
export const saveEmailAction = (payload) => ({
  type: SAVE_EMAIL,
  payload,
});
```


#### *Criar dentro do arquivo `redux/reducers/index.js`:*
- [ ] criar `rootReducer` usando o `combineReducers`
- [ ] exportar `rootReducer`

Exemplo:
```js
import { combineReducers } from 'redux';
import reducer1 from './reducer1';
import reducer2 from './reducer2';

const rootReducer = combineReducers({
  reducer1,
  reducer2,
});

export default rootReducer;
```
#### *Criar dentro dos demais arquivos do reducers (reducer1, reducer2, reducerNº) `redux/reducers/reducerNº` :*
- [ ] estado inicial
- [ ] criar função reducer com `switch` retornando apenas a opção `default`
- [ ] criar os casos para cada action criada, retornando o devido estado atualizado

```js
import { SAVE_EMAIL } from '../actions';

const INITIAL_STATE = { //colocar os estados iniciais
  //ex: email: '',
}; // Opcional

const reducer1 = (state = INITIAL_STATE, action) => {
 switch(action.type) {
 case SAVE_EMAIL:
   return {
     ...state,
     ...action.payload, // Ou ex: email: action.payload
   };
 default:
    return state;
 }
};

export default reducer1;
```

#### *Nos componentes que irão ler o estado:*
- [ ] criar a função `mapStateToProps`
- [ ] exportar usando o `connect`

#### *Nos componentes que irão modificar o estado:*
- [ ] criar a função `mapDispatchToProps`
- [ ] exportar usando o `connect`

Exemplo:

- *No import:*
```js
import PropTypes from 'prop-types';
import { connect } from 'react-redux';
```

- *Nos componentes que irão modificar o estado:*
```js
const mapDispatchToProps = (dispatch) => {(
  dispatchAddEmail: (email) => dispatch(saveEmailAction(email)),
});
// A utilização do mapDispatchProps é opcional já que o dispatch pode ser encontrado na props ficando assim por ex:
    const { dispatch } = this.props;
    const { email } = this.state;
    dispatch(saveEmailAction(email));
```
- *Nos componentes que irão ler o estado:*
```js
const mapStateToProps = (state) => ({
  email: state.email,
});
```

- *No export:*
```js
export default connect(mapStateToProps, mapDispatchToProps)(Component)
// Em caso de modificar e ler o estado
```

```js
export default connect()(Component);
// Quando apenas modifica o estado
```

```js
export default connect(mapStateToProps)(Component);
// Quando apenas lê o estado
```

