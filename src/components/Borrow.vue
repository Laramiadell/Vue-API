<template>
    <div>
        <div v-if="borrow!=null">
            <h1>{{borrow.student_id}}</h1>
            <div>
                {{borrow.books_id}}
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        borrow: null
    }
}
</script>

<style>
</style>