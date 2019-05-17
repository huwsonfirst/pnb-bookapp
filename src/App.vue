<template>
  <div id="app" class="small-container">
    <h1>Paper Nautilus Rare Books</h1>
    <book-form @add:book="addBook" />
    <book-table 
      :books="books" 
      @delete:book="deleteBook" 
      @edit:book="editBook"
    />
  </div>
</template>

<script>
import BookTable from '@/components/BookTable.vue'
import BookForm from '@/components/BookForm.vue'
export default {
  name: 'app',
  components: {
    BookTable,
    BookForm,
  },

  data() {
    return {
      books: [],
    }
  },

  mounted() {
    this.getBooks()
  },

  methods: {
    // addBook(book) {
    //   const lastId = 
    //     this.books.length > 0
    //       ? this.books[this.books.length - 1].id
    //       : 0;
    //   const id = lastId + 1;
    //   const newBook = { ...book, id };
    //   this.books = [...this.books, newBook];
    // },

    async addBook(book) {
      try {
        const response = await fetch('http://my-json-server.typicode.com/huwsonfirst/pnb-bookapp/books', {
          method: 'POST',
          body: JSON.stringify(book),
          headers: { 'Content-type': 'application/json; charset=UTF-8' },
        })
        const data = await response.json()
        this.books = [...this.books, data]
      } catch (error ) {
        // do something
      }
    },

    // editBook(id, updatedBook) {
    //   this.books = this.books.map(book =>
    //     book.id === id ? updatedBook : book
    //   )
    // },
    
  async editBook(id, updatedBook) {
    try {
      const response = await fetch(`http://my-json-server.typicode.com/huwsonfirst/pnb-bookapp/books/${id}`, {
        method: 'PUT',
        body: JSON.stringify(updatedBook),
        headers: { 'Content-type': 'application/json; charset=UTF-8' },
      })
      const data = await response.json()
      this.books = this.books.map(book =>
        (book.id === id ? data : book))
    } catch(error) {
      // do something
    }
  },

    // deleteBook(id) {
    //   this.books = this.books.filter(
    //     book => book.id !== id
    //   )
    // },

    async deleteBook(id) {
      try {
        await fetch(`http://my-json-server.typicode.com/huwsonfirst/pnb-bookapp/books/${id}`, {
          method: "DELETE"
        })
        this.books = this.books.filter(book =>
          book.id !== id)
      } catch(error) {
        // do something
      }
    },

    async getBooks() {
      try {
        const response = await fetch('http://my-json-server.typicode.com/huwsonfirst/pnb-bookapp/books')
        const data = await response.json()
        this.books = data
      } catch (error) {
        // do something
      }
    },
  }
}
</script>

<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }
  .small-container {
    max-width: 680px;
  }
</style>
