<template>

  <div id="app" class="container">

    <div class="page-header text-center">
      <h1>BOOK INVENTORY SYSTEM </h1>
    </div>
    
    <div class="card mt-3" >
      <div class="card-header">
        <h3>ADD A NEW BOOK</h3>
      </div>
      <div class="card-block mt-3 mb-3 font-weight-bold">

        <form id="form" v-on:submit.prevent="addBook">
          <div class="form-group ml-5 mr-5" >
            <label for="bookTitle">Title:</label>
            <input type="text" id="bookTitle" class="form-control" v-model="newBook.Title" placeholder="Title">
          </div>
           <div class="form-group ml-5 mr-5">
            <label for="bookAuthor">Author:</label>
            <input type="text" id="bookAuthor" class="form-control" v-model="newBook.Author" placeholder="Author">
          </div>
           <div class="form-group ml-5 mr-5">
            <label for="bookURL">URL:</label>
            <input type="text" id="bookURL" class="form-control" v-model="newBook.URL" placeholder="URL">
          </div>
          <input type="submit" class="btn btn-primary ml-5" value="Add Book"/>
        </form>
      </div>
    </div>

    <div class="card mt-3">
      <div class="card-header">
        <h3>LIST OF BOOKS</h3>
      </div>
      <div class="card-block">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>Title</th>
              <th>Author</th>
              <th>Delete</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="Book in Books">
              <td><a v-bind:href="Book.Url">{{Book.Title}}</a></td>
              <td>{{Book.Author}}</td>
              <td><span class="fas fa-trash-alt" v-on:click="removeBook(Book)"></span></td>
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
let bookRef = db.ref('Books');





export default {
  name: 'App',
  //data access
  firebase: {
    Books: bookRef
  },
  data () {
    return {
      newBook: {
        Title: '',
        Author: '',
        URL: ''
      }
    }
  },
  methods: {
    addBook: function() {
      bookRef.push(this.newBook);
      this.newBook.Title = '';
      this.newBook.Author = '';
      this.newBook.URL = '';
    },
    removeBook: function(book) {
      bookRef.child(book['.key']).remove();
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
