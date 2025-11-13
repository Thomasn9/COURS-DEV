<template>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cours-Dev</title>
    <!-- =========================================================================================================================== -->

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <NuxtLink to="/">
            <img id="logo" src="/logo.png" alt="Logo Cours Dev">
        </NuxtLink>
        <a class="navbar-brand" href="#">Cours Dev</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <li class="nav-item active">
                    <NuxtLink class="nav-link" to="/">Home</NuxtLink>
                </li>
                <li class="nav-item">
                    <NuxtLink class="nav-link" to="/JavaScript/index_javaSript">JavaScript</NuxtLink>
                </li>
                <li class="nav-item">
                    <NuxtLink class="nav-link" to="/PHP/index_php">PHP</NuxtLink>
                </li>
                <li class="nav-item">
                    <NuxtLink class="nav-link" to="/Java/index_java">Java</NuxtLink>
                </li>
                <li class="nav-item">
                    <NuxtLink class="nav-link" to="/SQL/index_sql">SQL</NuxtLink>
                </li>
                <li class="nav-item">
                    <NuxtLink class="nav-link" to="/cyber_securiter/index_cybersecu">Cyber Sécurité</NuxtLink>
                </li>
                <li class="nav-item">
                    <NuxtLink class="nav-link" to="/devops/index_devops">Devops</NuxtLink>
                </li>
                <!-- ===============================================\\FRAMEWORK//================================================= -->
                <li class="nav-item dropdown">
                <li class="nav-link dropdown-toggle" id="navbarDropdown" role="button" data-toggle="dropdown"
                    aria-haspopup="true" aria-expanded="false">
                    Framework
                </li>
                <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                    <NuxtLink class="dropdown-item" to="/vue/index_vue">Vue</NuxtLink>
                    <NuxtLink class="dropdown-item" to="#">React</NuxtLink>
                    <NuxtLink class="dropdown-item" to="#">Angular</NuxtLink>
                </div>
                </li>
                <!-- ===============================================\\META-FRAMEWORK//================================================= -->
                <li class="nav-item dropdown">
                <li class="nav-link dropdown-toggle" id="navbarDropdown" role="button" data-toggle="dropdown"
                    aria-haspopup="true" aria-expanded="false">
                    Meta Framework
                </li>
                <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                    <li>
                        <NuxtLink class="dropdown-item" to="#">Nuxt</NuxtLink>
                        <NuxtLink class="dropdown-item" to="#">Next</NuxtLink>
                    </li>
                </div>
                </li>
                                <!-- ===============================================\\Outils//================================================= -->
                <li class="nav-item dropdown">
                <li class="nav-link dropdown-toggle" id="navbarDropdown" role="button" data-toggle="dropdown"
                    aria-haspopup="true" aria-expanded="false">
                    Outils
                </li>
                <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                    <li>
                        <NuxtLink class="dropdown-item" to="/application/index_application">Application</NuxtLink>
                        <NuxtLink class="dropdown-item" to="#">Librairie </NuxtLink>
                        <NuxtLink class="dropdown-item" to="/services_web/index_services_web">Services Web</NuxtLink>
                    </li>
                </div>
                </li>
                <!-- ===============================================\\GESTION-PROJET//================================================= -->
                <li class="nav-item dropdown">
                <li class="nav-link dropdown-toggle" id="navbarDropdown" role="button" data-toggle="dropdown"
                    aria-haspopup="true" aria-expanded="false">
                    Gestion de projet
                </li>
                <div class="dropdown-menu" aria-labelledby="navbarDropdown">
                    <li>
                        <NuxtLink class="dropdown-item" to="/audit/index_audit">Diagramme UML</NuxtLink>
                        <NuxtLink class="dropdown-item" to="/audit/index_audit">Audit</NuxtLink>
                    </li>
                </div>
                </li>
            </ul>
        </div>
    </nav>
</template>

<script setup>
</script>

<style scoped>
#logo {
    width: 3vw;
    margin: 1cqw;
}
</style>