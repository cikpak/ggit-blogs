<template>
    <div>
        <h1>Blogul GGIT FD</h1>

        <div v-if="blogList.length > 0">
            <BlogItem
                v-for="blog in blogList"
                :key="blog.id"
                :id="blog.id"
                :user="blog.user"
                :post="blog.post"
                :likes="blog.likes"
                :tag="blog.tag"

                @like="likeHandler($event)"
                @dislike="dislikeHandler($event)"
            />
        </div>
        <div v-else>
            <p>𝓔𝓜𝓟𝓣𝓨</p>
        </div>

        <div>
            <input v-model="user"/>
            <textarea v-model="post"></textarea>
            <select v-model="tag">
                <option value="general">YEEEEEES</option>
                <option value="flame">FIREEEEE</option>
                <option value="recommendation">NOOOOOOO</option>
            </select>

            <button @click="submitFormHandler">Save</button>
        </div>

    </div>
</template>

<script>
import BlogItem from '../components/BlogItem.vue';
import { myaxios } from '../axios';
    export default {
        components: { BlogItem},
        data() {
            return {
                user: "",
                post: "",
                tag: "",
                blogList: []
            }
        },
        methods: {
            submitFormHandler(event){
                const newBlog = {
                    user: this.user,
                    post: this.post,
                    tag: this.tag
                }

                //Trimitem la backend obiectul nou

                myaxios.post("/blog", newBlog).then((response) =>{
                    this.blogList = response.data.blogs

                })

                console.log(newBlog)
            },

            fetchBlogPosts(){
                myaxios.get("/blog").then(
                    (response) => {
                        console.log(response.data.blogs)
                        this.blogList = response.data.blogs
                    }
                )
            },
            likeHandler(event){
                myaxios.post(`/blog/${event.itemId}/like`).then((response) => {
                        console.log(response.data.blogs)
                        this.blogList = response.data.blogs
                    })
            },
            dislikeHandler(event){
                console.log(event.itemId)
            }

        },
        mounted () {
            this.fetchBlogPosts()
        }
    }
</script>

<style lang="scss" scoped>

</style>