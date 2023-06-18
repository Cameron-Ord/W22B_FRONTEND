<template>
    <div>
        <header class="page_header">
            <div class="header_div">
                <h1>DEV.</h1>

                <span>
                    <router-link to="/login">Log In</router-link>
                    <router-link to="/signup">Sign Up</router-link>
            
                </span>

                <span>
                    <button @click="log_out">log out</button>
                </span>
            </div>
        </header>
    </div>
</template>

<script>
import axios from 'axios';
import Cookies from 'vue-cookies';
    export default {
        
        data() {
            return {
                
            }
        },

        methods:{

            log_out(){

                let current_token = Cookies.get('login_token');

                axios({
                    url:'http://127.0.0.1:5000/api/login',
                    method:'DELETE',

                    data:{

                        token: current_token

                    }
                }).then(res =>{

                    Cookies.remove('login_token')
                    this.$router.go('/')
                    res;

                }).catch(err =>{
                    err;

                });
            }

        },

        mounted(){


        }

    }
</script>

<style lang="scss" scoped>

</style>