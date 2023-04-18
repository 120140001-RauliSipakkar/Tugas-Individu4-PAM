# Tugas-Individu4-PAM

Nama: Rauli Sipakkar
Nim : 120140001

1. Implementasikan Redux Thunk dan Redux Saga yang memiliki fitur untuk menambahkan, menghapus, dan mengedit data. Buatlah beberapa aksi Redux yang berisi kode asynchronous, seperti melakukan HTTP request ke API.

import { connect } from 'react-redux';
import { addTodo } from '../actions';
import NewTodo from '../components/NewTodo';

const mapDispatchToProps = dispatch => {
  return {
    onAddTodo: todo => {
      dispatch(addTodo(todo));
    }
  };
};

export default connect(
  null,
  mapDispatchToProps
)(NewTodo);

import {
  ADD_TODO_SUCCESS,
  ADD_TODO_FAILURE,
  ADD_TODO_STARTED,
  DELETE_TODO
} from './types';

import axios from 'axios';

export const addTodo = ({ title, userId }) => {
  return dispatch => {
    dispatch(addTodoStarted());

    axios
      .post(`https://jsonplaceholder.typicode.com/todos`, {
        title,
        userId,
        completed: false
      })
      .then(res => {
        dispatch(addTodoSuccess(res.data));
      })
      .catch(err => {
        dispatch(addTodoFailure(err.message));
      });
  };
};

const addTodoSuccess = todo => ({
  type: ADD_TODO_SUCCESS,
  payload: {
    ...todo
  }
});

const addTodoStarted = () => ({
  type: ADD_TODO_STARTED
});

const addTodoFailure = error => ({
  type: ADD_TODO_FAILURE,
  payload: {
    error
  }
});

// ...

export const addTodo = ({ title, userId }) => {
  return dispatch => {
    dispatch(addTodoStarted());

    axios
      .post(ENDPOINT, {
        title,
        userId,
        completed: false
      })
      .then(res => {
        throw new Error('addToDo error!');
        // dispatch(addTodoSuccess(res.data));
      })
      .catch(err => {
        dispatch(addTodoFailure(err.message));
      });
  };
};

kode asynchronous
console.log('Hello')
console.log('Javascript')
console.log('Coder')

/*
Output :
Hello!
Javascipt
Coder
*/



2. **Perbandingan antara Redux Thunk dan Redux Saga**
**Redux **
Redux dapat juga diartikan sebagai suatu state management
terinspirasi oleh Flux

**Redux Thunk**
Redux Thunk merupakan Redux Thunk adalah middleware yang memungkinkan kita memanggil pembuat tindakan yang mengembalikan fungsi alih-alih objek tindakan. Fungsi tersebut menerima metode pengiriman toko, yang kemudian digunakan untuk mengirimkan tindakan sinkron reguler di dalam isi fungsi setelah operasi asinkron selesai. Dapat dikatakan sederhana, mudah dipelajari dan digunakan dengan volume 352B.
**Redux Thunk memiliki beberapa konsep yaitu sebagai berikut:**
-Periksa apakah tindakan tersebut adalah objek murni atau thunk
-Berikutnya meneruskan tindakan ke middleware jika itu adalah objek murni
-Luncurkan aksi jika itu adalah thunk
**Kelebihan Redux Thunk**
Yaitu  dapat memermudah pengiriman aksi yang mengikuti siklus hidup permintaan ke API eksternal.
**Kekurangan Redux Thunk**
yaitu dalam hal pengiriman metode tindakan yang ditemukan kurang sinkron

**Performance Redux Thunk**
var makeArray = function ()
{
   var temp = [];
   for(let i= 0, i < 10000; i++)    
   temp.push(i);
   return temp;
}

var e = makeArray();
var f = makeArray();

function test1()
{ var x = e.push(8);
}

var t2 = performance.now();

test1();

var t3 = performance.now();


t3-t2  //0.02

function test2()
{ var y = [...f, 8]
}


var t2 = performance.now();

test2();

var t3 = performance.now();


t3-t2 //1.98


**Sedangkan**

**Redux Saga**
Redux Saga memiliki fitur ES6 yang disebut Generator, memungkinkan kita menulis kode asinkron yang terlihat sinkron, dan sangat mudah untuk diuji. Dalam saga, kita dapat menguji aliran asinkron kami dengan mudah dan tindakan kami tetap murni. Tapi memiliki kerumitan, sulit dipelajari dan dipahami. Volume 14kB tetapi mengatur tindakan asinkron yang rumit dengan mudah dan membuatnya sangat mudah dibaca dan saga memiliki banyak alat yang berguna untuk menangani tindakan asinkron

**Kelebihan Redux Saga**
Yaitu jika dilakukan pengujian sangat mudah diuji
**Kekurangan Redux Saga**
Yaitu memiliki sedikit kerumitan dan kesulitan dalam memahami aliran asinkron
**Bagian Fitur saga**
import { put ) from 'redux-saga/effects'
import * as actions from '../actions/action'
import * as api from '../api/data'

function* data (action) {
  try {
    const {data} = yield api.data()
    yield put({ type: actions.MENAMPILKAN_DATA_SUCCESS, ...data })
  } catch (e) {
    yield put({ type: actions.MENAMPILKAN_DATA_FAILURE, e })
  }
}

export {
  data
}
Pada baris pertama terdapat import yang mengambil fungsi put dari redux-saga, fungsi put ini digunakan untuk mengganti atau meletakkan object didalam put pada action. Kemudian pada saga ini membutuhkan action dari app dan juga data yang akan diambil, sehingga pada baris dua dan tiga dilakukan import untuk mengambil action dan API.

Baris lima dalam pembuatan fungsi,  membubuhkan tanda * setelah kata function. Dalam saga ini dimasukkan dalam bagan try — catch yaa agar bisa mengetahui data yang dikembalikan, apabila pengambilan data pada API berhasil maka akan menuju action type pada baris delapan yaitu MENAMPILKAN_DATA_SUCCESS yang akan dihandle pada reducer. Begitu pula saat gagal mengambil data akan dihandle pada MENAMPILKAN_DATA_FAILURE, dan pada kasus diatas, tidak mengirimkan data apapun. 

3. Analisis dampak penggunaan Redux Thunk dan Redux Saga terhadap kualitas kode, seperti readability, maintainability, dan testability dan tes beberapa unit untuk menguji aksi Redux yang mengandung kode asynchronous.

console.log('Hello')
console.log('Javascript')
console.log('Coder')

/*
Output :
Hello!
Javascipt
Coder
*/
