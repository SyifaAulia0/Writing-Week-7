# Writing-Week-7
## React Context
- React context bukan state management
- react context seperti redux, menyelesaikan masalah props drilling, tetapi react context membuat sebuah data yang bersifat global 
cara buatnya :
buat conteksnya, import react create context
bungkus app dengan parent provider
panggil nama context (keranjangcountcontext) pakai usecontext

counter akan dipangiil react-context
counterprovider buat const countercontext = createcontext
context nya ditaruh di countercontext.provider
provider akan menerima children, dipanggil di countercontext.provider
counterprovider sebagai pembungkus app di main.jsx
- ada 2 cara
  1. oper data ke dalam component home
  2. oper component ke dalam component (children, parent) app dibungkus dengan keranjangCountProvider




useReducer
import useReducer
buat function reducer(state, action)
buat switch case 
panggil useReducer di dalam function counterprovider
buat action untuk mengubah state
increment, decrement
buat const increment, decrement

context biasa untuk menglobalkan datanya
dengan bantuan reducer, datanya bisa di manage

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
