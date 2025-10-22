<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <a class="navbar-brand" href="#">Projet Cours Dev</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item active">
                    <a class="nav-link" href="/index">Home <span class="sr-only">(current)</span></a>
                </li>
                <li class="nav-item">
                    <a class="nav-link"><NuxtLink to="/PHP">JavaScript</NuxtLink></a>
                </li>
                <li class="nav-item">
                    <a class="nav-link"><NuxtLink to="/PHP">PHP</NuxtLink></a>
                </li>
                <li class="nav-item">
                    <a class="nav-link"><NuxtLink to="/PHP">Java</NuxtLink></a>
                </li>
<!-- ===============================================\\FRAMEWORK//================================================= -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button"
                        data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        Framework
                    </a>
                    <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                        <a class="dropdown-item"><NuxtLink to="/PHP/coucou">Vue</NuxtLink></a>
                        <a class="dropdown-item"><NuxtLink to="/PHP/coucou">React</NuxtLink></a>
                        <a class="dropdown-item"><NuxtLink to="/PHP/coucou">Angular</NuxtLink></a>
                    </div>
                </li>
<!-- ===============================================\\META-FRAMEWORK//================================================= -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button"
                        data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        Meta Framework
                    </a>
                    <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                        <a class="dropdown-item"><NuxtLink to="/PHP/coucou">Nuxt</NuxtLink></a>
                        <a class="dropdown-item"><NuxtLink to="/PHP/coucou">Next</NuxtLink></a>
                    </div>
                </li>
            </ul>
        </div>
    </nav>
</template>

<script setup>
// Votre code JavaScript ici si nécessaire
</script>