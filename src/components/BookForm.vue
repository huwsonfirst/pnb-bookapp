<template>
    <div id="book-form">
        <form @submit.prevent="handleSubmit">
            <label>Author Name</label>
            <input 
                ref="author"
                :class="{ 'has-error': submitting && invalidAuthor }"
                v-model="book.author" 
                @focus="clearStatus"
                @keypress="clearStatus"
                type="text" 
            />
            <label>Book Title</label>
            <input
                ref="title"
                :class="{ 'has-error': submitting && invalidTitle }" 
                v-model="book.title" 
                type="text"
                @focus="clearStatus"
            />
            <p v-if="error && submitting" class="error-message">
                Please fill out all required fields </p>
            <p v-if="success" class="success-message">
                Book successfully added! </p>
            <button>Add Book</button>
        </form>
    </div>
</template>

<script>
export default {
    name: 'book-form',
    data() {
        return {
            submitting: false,
            error: false,
            success: false,
            book: {
                author: '',
                title: '',
            },
        }
    },
    methods: {
        handleSubmit() {
            this.submitting = true
            this.clearStatus()

            if(this.invalidAuthor) {
                this.$refs.author.focus()  
                this.error = true
                return
            }

            if(this.invalidTitle) {
                this.$refs.title.focus()
                this.error = true
                return
            }

            this.$emit('add:book', this.book)
            this.book = {
                author: '',
                title: '',
            }
            this.$refs.first.focus();

            this.error = false
            this.success = true
            this.submitting = false
        },

        clearStatus() {
            this.success = false
            this.error = false
        }
    },
    computed: {
        invalidAuthor() {
            return this.book.author === ''
        },
        invalidTitle() {
            return this.book.title === ''
        },
    },
}
</script>

<style scoped>
form {
    margin-bottom: 2rem;
}

[class*='-message'] {
    font-weight: 500;
}

.error-message {
    color: #d33c40;
}

.success-message {
    color: #32a95d;
}
</style>


