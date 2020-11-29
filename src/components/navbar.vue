<template>
    <nav>
        <a href="#">to-do app</a>
        <a href="#">posts</a>
        <a href="#">photos</a>
    </nav>
</template>

<script>
export default {
    
}
</script>

<style scoped>
 nav {
     display: flex;
     justify-content: space-between;
     margin: 0 20%;
 }
 a {
     text-decoration: none;
     color: #2c3e50;
     font-size: 20px;
 }
 a:hover {
     color:coral;
 }
</style>