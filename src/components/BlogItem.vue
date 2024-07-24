<template>
    <div>
        <h5>{{user}}</h5>
        <p>{{post}}</p>

        <img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fi.redd.it%2Fel37guwk9js21.jpg&f=1&nofb=1&ipt=8d288374f1dff8c5e4d2baaa8e62011ef5b34c06ec7650501609c955705fa01d&ipo=images">
        <div>
            <button @click="likeItem">GOOD</button>
            <p>{{likes}}</p>
            <button @click="dislikeItem">BAD</button>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            id: Number,
            user: String,
            post: String,
            likes: Number,
            tag: String
        },
        emits: ['like', 'dislike'],
        methods: {
            likeItem(){
                this.$emit("like", {itemId: this.id})
            },
            dislikeItem(){
                this.$emit("dislike", {itemId: this.id})
            }
        }
    }
</script>

<style scoped>

</style>