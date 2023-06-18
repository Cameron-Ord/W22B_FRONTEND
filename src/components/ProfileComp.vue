<template>
    <div v-if="prof_data !==undefined">

        <h2>Welcome, {{ prof_data['username'] }}</h2>

        <img v-bind:src="prof_data['image_url']" alt="an image">

        <h3>Email: {{ prof_data['email'] }}</h3>

        <h3>Bio: {{ prof_data['bio'] }}</h3>

    </div>
</template>

<script>
import Cookies from 'vue-cookies';
import axios from 'axios';
    export default {
        
        data() {
            return {
                status: undefined,
                token_var: undefined,
                prof_data: undefined
            }
        },

        methods:{

            on_mount(){

                axios({

                    url: 'http://127.0.0.1:5000/api/client',
                    method: 'GET',

                    params:{

                        token: this.token_var
                    }
                }).then(res =>{

                    this.prof_data = res['data'][0];
                    console.log(res);


                }).catch(err =>{

                    this.status = 'something went wrong, try again.';
                    err;
                })

            }
        },

        mounted(){

            this.token_var = Cookies.get('login_token');


            this.on_mount();

          
        }
    }
</script>

<style lang="scss" scoped>

</style>