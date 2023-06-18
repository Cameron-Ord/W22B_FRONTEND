<template>
    <div>
        <article>
            <div>

                <input type="text" placeholder="username" ref="username">
                <input type="password" placeholder="password" ref="password">

                <button @click="login_form">Log In</button>
            </div>
        </article>
    </div>
</template>

<script>
import axios from 'axios';
import Cookies from 'vue-cookies';
    export default {
        
        data() {
            return {
                status: undefined
            }
        },

        methods:{

            login_form(){

                axios({
                    url:'http://127.0.0.1:5000/api/login',
                    method: 'POST',

                    data:{

                        username: this.$refs['username'].value,
                        password: this.$refs['password'].value


                    }


                }).then(res =>{

                    console.log(res)
                    Cookies.set('login_token', `${res['data'][0]['token']}`);
                    this.$router.push('/')

                }).catch(err =>{

                    err;
                    this.status = 'invalid login, try again.';


                })
            }

        },


        mounted(){


        }
    }
</script>

<style lang="scss" scoped>

</style>