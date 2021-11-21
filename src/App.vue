<template>
    <div id="app">
        <Main></Main>
    </div>
</template>

<script>
import Main from './components/Main.vue'

export default {
    name: 'App',
    components: {
        Main
    }
}
</script>

<style>
html,body,#app{
display:grid;
height:100%;
}
body{
  margin:0;
  width:100%;
}
#app {
    background-color: #000;
    color: white;
    font-family: 'Roboto' ;
  
}

</style>
