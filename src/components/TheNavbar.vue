<template>
    <nav class="navbar bg-body-green">
    <div class="container-fluid">
        <a class="navbar-brand" href="#">
        <img src="../assets/logo.png" alt="Logo" width="30" height="24" class="d-inline-block align-text-top">
            VueInterface Website 
        </a>
    </div>
    </nav>
</template>

<script>
    export default{
    }
</script>

<style>

.navbar-brand{
    color: var(--charcoal-2);
    transition: all .5s ease;
}

.navbar-brand:hover{
    color: var(--charcoal);
}

.bg-body-green{
    background-color: var(--mint-2);
}



</style>