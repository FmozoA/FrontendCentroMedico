<template>
    <div class="signUp_user">
        <div class="container_signUp_user">
            <h2>Registro de usuario</h2>
            <form v-on:submit.prevent="processSignUp">
                <input type="text"  v-model="user.username" placeholder="Nombre de usuario">
                <br>
                <input type="password" v-model="user.password" placeholder="Contraseña">
                <br>
                <input type="text" v-model="user.name" placeholder="Nombre">
                <br>
                <input type="email" v-model="user.email" placeholder="Correo Electrónico">
                <br>
                <button type="submit">Registrarse</button>
            </form>   
        </div>
    </div>
</template>

<script>
import axios from 'axios'    
export default {
    name: 'SignUp',
    data:function(){
        return{
            user:{
                username:"",
                password:"",
                name:"",
                email:"",
                account:{
                    balance:0,
                    isActive: true,
                    lastChangeDate: (new Date()).toJSON().toString()
                }
            }
        }    
    },
    methods:{
        processSignUp:function(){
            axios.post(
                "https://mision-tic-g1-backend.herokuapp.com/userCreate/",
                this.user,
                {headers:{}}
            )
            .then((result)=>{
                let dataSignUp = {
                    username: this.user.username,
                    token_access: result.data.access,
                    token_refresh: result.data.refresh
                }
                this.$emit('completedSignUp',dataSignUp)
            })
            .catch((error)=> {
                console.log(error)
                alert("Error en la creación del usuario")
            })
        }    
    }    
}
</script>

<style>
    .signUp_user{
        margin: 0;
        padding: 0%;
        height: 100%;
        width: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
     }
     .container_signUp_user {
        border: 3px solid #283747;
        border-radius: 10px;
        width: 25%;
        height: 70%;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }
    .signUp_user h2
    {
        color: #283747;
    
    }
     .signUp_user form
    {
        width: 70%;
    }
     .signUp_user input
    {
        height: 40px;
        width: 100%;
        box-sizing: border-box;
        padding: 10px 20px;
        margin: 5px 0;
        border: 1px solid #283747;
    
    }
     .signUp_user button
    {
        width: 100%;
        height: 40px;
        color: #E5E7E9;
        background: #283747;
        border: 1px solid #E5E7E9;
        border-radius: 5px;
        padding: 10px 25px;
        margin: 5px 0 25px 0;
    }
     .signUp_user button:hover {
        color: #E5E7E9;
        background: crimson;
        border: 1px solid #283747;
     }
    
    </style>