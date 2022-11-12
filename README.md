# Writing-Week-7
## React Context
- React context bukan state management
- react context seperti redux, menyelesaikan masalah props drilling, tetapi react context membuat sebuah data yang bersifat global 
- cara buat react context :
  1. buat conteksnya, import react create context
  2. bungkus app dengan parent provider
  3. panggil nama context (keranjangcountcontext) pakai usecontext
  4. counter akan dipangil react-context
  5. counterprovider buat const countercontext = createcontext
  6. context nya ditaruh di countercontext.provider
  7. provider akan menerima children
  ```jsx
  import React, { createContext, useState } from 'react'

  export const KeranjangCountContext = createContext()

  function KeranjangCountProvider({children}) {
  const [keranjangCount, setKeranjangCount] = useState(0)

  return (
    <KeranjangCountContext.Provider value={{keranjangCount, setKeranjangCount}}>
      {children}
    </KeranjangCountContext.Provider>
  )
  }

  export default KeranjangCountProvider
  ```
  8. counterprovider sebagai pembungkus app di main.jsx
  ```jsx
  import React from "react";
  import ReactDOM from "react-dom/client";
  import App from "./App";
  import KeranjangCountProvider from "./KeranjangCountProvider";
  import UserProvider from "./UserProvider";

  ReactDOM.createRoot(document.getElementById("root")).render(
  // <React.StrictMode>
  <UserProvider>
    <KeranjangCountProvider>
      <App />
    </KeranjangCountProvider>
  </UserProvider>
  // </React.StrictMode>
  );
  ```
### useReducer
- context biasa untuk menglobalkan datanya, dengan bantuan reducer datanya bisa di manage
1. import useReducer
2. buat function reducer(state, action)
3. buat switch case 
4. panggil useReducer di dalam function counterprovider
5. buat action untuk mengubah state 
6. buat const increment, decrement
```jsx
//Counter1Provider.jsx
import React, { createContext, useReducer, useState } from "react";

export const CounterContext = createContext();

function Counte1Provider({ children }) {
  const [count, setCount] = useState(0)

  return (
    <CounterContext.Provider value={{ count, setCount }}>
      {children}
    </CounterContext.Provider>
  );
}

export default Counte1Provider;

//Counter2Provider.jsx
import React, { createContext, useReducer, useState } from "react";

export const CounterContext = createContext();

const INCREMENT = "INCREMENT";
const DECREMENT = "DECREMENT";

const initialState = {
  count: 0,
};

function reducer(state, action) {
  switch (action.type) {
    case INCREMENT:
      return { count: state.count + 1 };
    case DECREMENT:
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter2Provider({ children }) {
  const [state, dispatch] = useReducer(reducer, initialState);

  const increment = () => {
    dispatch({ type: INCREMENT });
  };

  const decrement = () => {
    dispatch({ type: DECREMENT });
  };

  return (
    <CounterContext.Provider value={{ state, increment, decrement }}>
      {children}
    </CounterContext.Provider>
  );
}

export default Counter2Provider;

```
```jsx
//main.jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import Counter2Provider from "./context/Counter2Provider";
import Counter1Provider from "./context/Counter1Provider";
import TodoProvider from "./context/TodoProvider";

ReactDOM.createRoot(document.getElementById("root")).render(
  // <React.StrictMode>
  <TodoProvider>
    <Counter2Provider>
      <Counter1Provider>
        <App />
      </Counter1Provider>
    </Counter2Provider>
  </TodoProvider>
  // </React.StrictMode>
);
```
## React Testing
react teating

manual testing : necek sendiri/manual
unit test : mnguji kode yang paling kecil
integration : melakukan pengujian jika terhubung ke apk lain, c/o database
end to end : secara ssi user

jest : lib js untuk melakukan test
rtl : react testing lib, sudah include jest

ada 2 cara
TDD
test faills
test passes
refact: memperbagus kode

buat kode testing lama, apk harus jelas, speksi harus jelas

pake app node versi 16
install jest
buat file app
bikin ekspektasi di app
buat kode test
export sum di app.js
dijalanin : npm run test

coverage : seberapa persen codingan kita masuk kedala testing

rtl
ngebantu testing sebuah ui dari sudut pandang user

ngerender comp
ambil component pakai screen.getbytext
learn reactada di app.js
ekpektasi : link element ada didlm documment
npm run test

pola di rtl
buat pola test  block
