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
- type testing :
1. manual testing : ngecek sendiri/manual dengan console.log
2. 2. automayion : kode testing
- ada 3 tingaktan dalam react testing, berikut adalah urutan dari yang terbawah sampai terataas :
1. unit test : menguji kode yang paling kecil
2. integration : melakukan pengujian jika terhubung ke apk lain, c/o database
3. end to end : secara sisi user
- semakin ke atas biayanya semakin mahal, yang dibutuhkan juga semakin banyak

- jest : library js untuk melakukan test
- rtl : react testing lib, sudah include jest
- ada 2 cara testing :
1. buat fitur lalu testing
2. testing dahulu, kemudian buat fitur
### TDD
- TDD : testing dahulu, kemudian buat fitur
- TDD circle of life : test fails(membuat ekspektasi), test passes(membuat kode), refact (memperbagus kode)
- buat kode testing lama, apk harus jelas, spesifikasi harus jelas apa yang mau dibuat
- cara melakukan testing dengan react, dan metode TDD : 
1. install jest
2. buat file app
3. bikin ekspektasi di app
4. buat kode test
5. export di app.js
6. dijalanin : npm run test
- coverage : seberapa persen codingan kita masuk kedala testing
- rtl fungsinya untuk membantu testing sebuah ui dari sudut pandang user


