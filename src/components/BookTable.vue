<template>
    <div id="book-table">
        <p v-if="books.length < 1" class="empty-table">
            No Books...
        </p>
        <table v-else>
            <thead>
                <tr>
                    <th>Author Name</th>
                    <th>Book Title</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="book in books" :key="book.id">
                    <td v-if="editing === book.id">
                        <input type="text" v-model="book.author" />
                    </td>
                    <td v-else>{{ book.author }}</td>
                    <td v-if="editing === book.id">
                        <input type="text" v-model="book.title" />
                    </td>
                    <td v-else>{{ book.title }}</td>
                    <td v-if="editing === book.id">
                        <button @click="editBook(book)">Save</button>
                        <button class="muted-button" @click="editing = null">Cancel</button>
                        
                    </td>
                    <td v-else>
                        <button @click="editMode(book.id)">Edit</button>
                        <button @click="$emit('delete:book', book.id)">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        name: 'book-table',
        props: {
            books: Array,
        },
        data() {
            return {
                editing: null,
            }
        },
        methods: {
            editMode(id) {
                this.editing = id
            },
            editBook(book) {
                if(book.author === '' || book.title === '') return
                this.$emit('edit:book', book.id, book)
                this.editing = null
            },
        },
    }
</script>

<style scoped>
button {
    margin: 0 0.5rem 0 0;
}
</style>