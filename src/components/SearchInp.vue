<template>
    <form class="container-fluid d-flex justify-content-center mt-5" role="search">
    <div class="input-group w-50">
        <button class="input-group-text" id="basic-addon1" type="submit"><i class="fa-solid fa-magnifying-glass text-muted"></i></button>
        <input class="form-control me-2 bg-white" type="search" placeholder="Buscar Cadastros de Operadoras" aria-label="Buscar Cadastros de Operadoras" aria-describedby="basic-addon1">
    </div>
    </form>
</template>

<script>
    export default{
    }
</script>

<style>
    input.bg-white{
        background-color: var(--input-bg-color) !important;
    }

    button, input{
        padding: .9rem !important;
    }

    button{
        padding: .9rem 1.5rem !important;
    }

</style>