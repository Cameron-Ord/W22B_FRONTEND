<template>
    <div>
        <page-header></page-header>
        <article>
            <div>

                <input type="text" placeholder="email" ref="email">

                <input type="text" placeholder="username" ref="user">
                
                <input type="password" placeholder="password" ref="pass">
                
                <input type="text" placeholder="bio" ref="bio">
                
                <input type="text" placeholder="profile image" ref="image_url">

                <button @click="usersignup">signup</button>

                <p v-if="status !== undefined">{{ status }}</p>
            </div>
        </article>
    </div>
</template>

<script>
import PageHeader from '@/components/PageHeader.vue';
import axios from 'axios';

    export default {
        components:{
            PageHeader
        },


        data() {
            return {

                status: undefined

            }
        },

        methods:{

            usersignup(){


                axios({
                    url:'http://127.0.0.1:5000/api/client',

                    method: 'POST',

                    data:{

                        username: this.$refs['user'].value,
                        email: this.$refs['email'].value,
                        password: this.$refs['pass'].value,
                        bio: this.$refs['bio'].value,
                        image_url: this.$refs['image_url'].value

                    }
                }).then(response => {

                    this.status = 'success!';
                    console.log(response);
                    this.$router.push(`/`)

                }).catch(error => {

                    error;

                    this.status = 'something went wrong';
                })

            }


        },

        mounted(){


        }
    }
</script>

<style lang="scss" scoped>

</style>