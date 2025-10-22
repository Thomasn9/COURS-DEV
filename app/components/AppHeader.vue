<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <img id="logo" src="/logo.png" alt="">
        <a class="navbar-brand" href="#">Cours Dev</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item active">
                    <a class="nav-link"><NuxtLink to="/">Home</NuxtLink></a>
                </li>
                <li class="nav-item">
                    <a class="nav-link"><NuxtLink to="#">JavaScript</NuxtLink></a>
                </li>
                <li class="nav-item">
                    <a class="nav-link"><NuxtLink to="/PHP/index_php">PHP</NuxtLink></a>
                </li>
                <li class="nav-item">
                    <a class="nav-link"><NuxtLink to="#">Java</NuxtLink></a>
                </li>
                <li class="nav-item">
                    <a class="nav-link"><NuxtLink to="#">SQL</NuxtLink></a>
                </li>
<!-- ===============================================\\FRAMEWORK//================================================= -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" id="navbarDropdown" role="button"
                        data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        Framework
                    </a>
                    <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                        <a class="dropdown-item"><NuxtLink to="#">Vue</NuxtLink></a>
                        <a class="dropdown-item"><NuxtLink to="#">React</NuxtLink></a>
                        <a class="dropdown-item"><NuxtLink to="#">Angular</NuxtLink></a>
                    </div>
                </li>
<!-- ===============================================\\META-FRAMEWORK//================================================= -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" id="navbarDropdown" role="button"
                        data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        Meta Framework
                    </a>
                    <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                        <a class="dropdown-item"><NuxtLink to="#">Nuxt</NuxtLink></a>
                        <a class="dropdown-item"><NuxtLink to="#">Next</NuxtLink></a>
                    </div>
                </li>
            </ul>
        </div>
    </nav>
</template>

<script setup>
// Votre code JavaScript ici si nécessaire
</script>

<style scoped>
#logo{
    width: 3vw;
    margin: 1cqw;
}
</style>