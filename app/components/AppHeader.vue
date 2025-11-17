<template>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cours-Dev</title>

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

                <!-- ===============================================\\LANGAGES//================================================= -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownLangages" role="button"
                        data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        Langages
                    </a>
                    <div class="dropdown-menu" aria-labelledby="navbarDropdownLangages">
                        <NuxtLink class="dropdown-item" to="langages/Java/index_java">Java</NuxtLink>
                        <NuxtLink class="dropdown-item" to="langages/JavaScript/index_javaSript">JavaScript</NuxtLink>
                        <NuxtLink class="dropdown-item" to="langages/PHP/index_php">PHP</NuxtLink>
                        <NuxtLink class="dropdown-item" to="langages/SQL/index_sql">SQL</NuxtLink>
                    </div>
                </li>

                <!-- ===============================================\\FRAMEWORK//================================================= -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownFramework" role="button"
                        data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        Framework
                    </a>
                    <div class="dropdown-menu" aria-labelledby="navbarDropdownFramework">
                        <NuxtLink class="dropdown-item" to="/vue/index_vue">Vue</NuxtLink>
                        <NuxtLink class="dropdown-item" to="#">React</NuxtLink>
                        <NuxtLink class="dropdown-item" to="#">Angular</NuxtLink>
                        <div class="dropdown-divider"></div>
                        <NuxtLink class="dropdown-item" to="/boostrap/index_boostrap">Bootstrap</NuxtLink>
                        <NuxtLink class="dropdown-item" to="/tailwind_css/index_tailwind_css">Tailwind CSS</NuxtLink>
                    </div>
                </li>

                <!-- ===============================================\\META-FRAMEWORK//================================================= -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMeta" role="button"
                        data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        Meta Framework
                    </a>
                    <div class="dropdown-menu" aria-labelledby="navbarDropdownMeta">
                        <NuxtLink class="dropdown-item" to="#">Nuxt</NuxtLink>
                        <NuxtLink class="dropdown-item" to="#">Next</NuxtLink>
                    </div>
                </li>

                <!-- ===============================================\\Outils//================================================= -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownOutils" role="button"
                        data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        Outils
                    </a>
                    <div class="dropdown-menu" aria-labelledby="navbarDropdownOutils">
                        <NuxtLink class="dropdown-item" to="/application/index_application">Application</NuxtLink>
                        <NuxtLink class="dropdown-item" to="/librairie/index_librairie">Librairie</NuxtLink>
                        <NuxtLink class="dropdown-item" to="/services_web/index_services_web">Services Web et Design
                        </NuxtLink>
                    </div>
                </li>

                <!-- ===============================================\\GESTION-PROJET//================================================= -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownGestion" role="button"
                        data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                        Gestion de projet
                    </a>
                    <div class="dropdown-menu" aria-labelledby="navbarDropdownGestion">
                        <NuxtLink class="dropdown-item" to="/audit/index_audit">Diagramme UML</NuxtLink>
                        <NuxtLink class="dropdown-item" to="/audit/index_audit">Outils</NuxtLink>
                        <NuxtLink class="dropdown-item" to="/audit/index_audit">Audit et Testing</NuxtLink>
                    </div>
                </li>

                <li class="nav-item">
                    <NuxtLink class="nav-link" to="/cyber_securiter/index_cybersecu">Cyber Sécurité</NuxtLink>
                </li>
                <li class="nav-item">
                    <NuxtLink class="nav-link" to="/devops/index_devops">Devops</NuxtLink>
                </li>
                <li class="nav-item">
                    <NuxtLink class="nav-link" to="/mise_en_place_projet/index_mise_en_place_projet">Mise en place projet</NuxtLink>
                </li>

            </ul>
        </div>
    </nav>
</template>

<script setup>
</script>

<style scoped>
#logo {
    width: 4vw;
    margin: 1cqw;
}
/* Responsive adjustments */
@media (max-width: 1000px) {
    #logo {
        width: 12vw ;
    }
}

.navbar-brand {
    margin-left: 10px;
}
</style>