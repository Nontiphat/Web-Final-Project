<template>
<!-- new navbar -->
<div class="navbar navbar-inverse navbar-fixed-top">
    <div class="container">
        <div class="navbar-header">
            <a class="navbar-brand navbar-link" href="#" v-on:click.prevent="navigateTo('/dashboard')">
                <img src="../assets/3829187415_175d7b5c-a417-40ae-ac27-dacf8a95ff03.png" id="logo">
            </a>
            <button class="navbar-toggle collapsed" data-toggle="collapse" data-target="#navcol-1">
                <span class="sr-only">Toggle navigation</span>
                <span class="icon-bar"></span><span class="icon-bar"></span>
                <span class="icon-bar"></span>
            </button>
        </div>
        <div class="collapse navbar-collapse" id="navcol-1">
            <ul class="nav navbar-nav navbar-right">
                <li role="presentation"><router-link :to="{name: 'products'}">Notebook</router-link></li>
                <li><router-link :to="{name: 'users'}" >Users</router-link></li>
                <li><router-link :to="{name: 'Cartlist'}" >Cartlist</router-link></li>
                <li v-if="!isUserLoggedIn"><router-link :to="{name: 'login'}" >Login</router-link></li>
                <transition name="fade">
                    <li v-if="isUserLoggedIn" role="presentation"><a href="#">{{user.name}}</a></li>
                </transition>
                <li v-if="isUserLoggedIn" role="presentation"><a href="#" v-on:click.prevent="logout">Logout</a></li>
            </ul>
        </div>
    </div>
    <!-- old navbar 
    <div class="nv-navbar">
    <ul class="nav">
    <li><router-link :to="{name: 'blogs'}" >Blogs</router-link></li>
    <li><router-link :to="{name: 'users'}" >Users</router-link></li>
    <li><router-link :to="{name: 'comments'}" >Comments</router-link></li>
    <li><router-link :to="{name: 'login'}" >Login</router-link></li>
    <li><a href="#" v-on:click="logout">Logout</a></li>
    </ul>
    <div class="clearfix"></div>
    </div>-->
</div>

</template>
<script>
import {mapState} from 'vuex'
export default {
    methods: {
        logout () {
            this.$store.dispatch('setToken', null)
            this.$store.dispatch('setBlog', null)
            this.$router.push({
                name: 'login'
            })
        }
    },
    computed: {
        ...mapState([
            'isUserLoggedIn',
            'user'
        ]),
    },
}
</script>
<style scoped>
    .nv-navbar {
        background-color:palegoldenrod;
        width: 100%;
        padding:10px 0px 10px 0px;
    }

    .nv-navbar .nav {
        list-style: none;
        margin:0;
        padding:0;
        float:left;
    }

    .nv-navbar .nav li {
        float:left;
    }

    .nv-navbar .nav li a {
        padding: 10px;
        text-decoration: none;
        color:gray;
        font-weight: bold;
    }

    .nv-navbar .nav li a:hover {
        padding: 10px;
        text-decoration: none;
        color:darkslategrey;
    }

    .nv-navbar .nav li a.router-link-active {
        background-color:gold;
        color:darkslategrey;
    }

    .navbar-brand > img {
        width: 40px;
  padding: 12px 0;
  margin-top: -20px;
    }
    a.router-link-active{
        color:rgb(0, 217, 255) !important;
    } 
    .navbar-inverse {
        background-color: rgb(51, 24, 24);
        border-color: #080808;
    }
 </style>