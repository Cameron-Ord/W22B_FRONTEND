<template>
    <div>
        <header class="page_header">
            <div class="header_div">
                <h1>DEV.</h1>

                <span>
                    <router-link to="/login">Log In</router-link>
                    <router-link to="/signup">Sign Up</router-link>
            
                </span>

                <span v-if="current_token !== null">
                    <button @click="log_out">Log Out</button>
                    <router-link to="/profile">Profile</router-link>
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
                current_token: undefined
            }
        },

        methods:{

            log_out(){

                

                axios({
                    url:'http://127.0.0.1:5000/api/login',
                    method:'DELETE',

                    data:{

                        token: this.current_token

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

            this.current_token = Cookies.get('login_token');
        }

    }
</script>

<style lang="scss" scoped>

</style>