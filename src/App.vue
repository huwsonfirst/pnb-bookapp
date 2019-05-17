<template>
  <div id="app" class="small-container">
    <h1>Paper Nautilus Rare Books</h1>
    <book-form @add:book="addBook" />
    <book-table :books="books" @delete:book="deleteBook" />
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
  methods: {
    addBook(book) {
      const lastId = 
        this.books.length > 0
          ? this.books[this.books.length - 1].id
          : 0;
      const id = lastId + 1;
      const newBook = { ...book, id };
      this.books = [...this.books, newBook];
    },
    
    deleteBook(id) {
      this.books = this.books.filter(
        book => book.id !== id
      )
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
