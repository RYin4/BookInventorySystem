<template>
  <div id="app" class="container">
    <div class="page-header">
      <h1>Vue.js 2 and Firebase Sample Application </h1>
    </div>
    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>Books Lists</h3>
      </div>
      <div class="panel-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>
                Title
              </th>
              <th>
                Author
              </th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="book in books">
              <td>
                <a v-bind:href="book.url">{{book.title}}</a>
              </td>
              <td>
                {{book.author}}
              </td>

            </tr>
          </tbody>
        </table>
        </div>
    </div>


  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import Firebase from 'firebase'

//access to the firebase api 
let config = {
    apiKey: "AIzaSyDyG2Ximhha4c0g1D_yVX0pPegbxuxGctM",
    authDomain: "vuejs-firebase-dac4d.firebaseapp.com",
    databaseURL: "https://vuejs-firebase-dac4d.firebaseio.com",
    projectId: "vuejs-firebase-dac4d",
    storageBucket: "vuejs-firebase-dac4d.appspot.com",
    messagingSenderId: "755924921672"
}

//establish connection to firebase
let app = Firebase.initializeApp(config);
let db = app.database();

//ref to books node in the firebase db
let bookRef = db.ref('books');





export default {
  name: 'App',
  //data access
  firebase: {
    books: booksRef
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
