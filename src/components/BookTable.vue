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
                    <td>{{ book.author }}</td>
                    <td>{{ book.title }}</td>
                    <td>
                        <button>Edit</button>
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
    }
</script>

<style scoped>
button {
    margin: 0 0.5rem 0 0;
}
</style>