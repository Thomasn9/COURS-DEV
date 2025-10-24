<template class="h-200">
    <header class="bg-dark text-white py-4">
        <h1 class="display-4 fw-bold">Bienvenue sur le recueil de cours</h1>
        <p class="lead">Ma plateforme d'apprentissage des technologies web</p>
    </header>

    <main class="container-fluid py-5 bg-black">
        <div class="row justify-content-center g-4">
            <div class="col-md-4 col-lg-3">
                <div class="card bg-dark text-white border-purple shadow-lg h-100">
                    <img class="card-img" src="/img_index/php.png" alt="Logo PHP">
                    <div class="card-body d-flex flex-column">
                        <h5 class="card-title text-purple fw-bold">La doc officielle de PHP</h5>
                        <p class="card-text text-light flex-grow-1">Toute la doc officielle de PHP si jamais les exemples présents sur le recueil ne suffisent pas !</p>
                        <a href="https://www.php.net/docs.php" class="btn btn-purple mt-auto">Aller au site</a>
                    </div>
                </div>
            </div>
            
            <div class="col-md-4 col-lg-3">
                <div class="card bg-dark text-white border-purple shadow-lg h-100">
                    <img class="card-img" src="/img_index/js.png" alt="Logo JavaScript">
                    <div class="card-body d-flex flex-column">
                        <h5 class="card-title text-purple fw-bold">La doc de JavaScript</h5>
                        <p class="card-text text-light flex-grow-1">Ici se trouve la doc officielle de JavaScript</p>
                        <a href="#" class="btn btn-purple mt-auto">Aller au site</a>
                    </div>
                </div>
            </div>
            
            <div class="col-md-4 col-lg-3">
                <div class="card bg-dark text-white border-purple shadow-lg h-100">
                    <img class="card-img" src="/img_index/java.png" alt="Logo Java">
                    <div class="card-body d-flex flex-column">
                        <h5 class="card-title text-purple fw-bold">Java</h5>
                        <p class="card-text text-light flex-grow-1">La doc officielle de Java</p>
                        <a href="#" class="btn btn-purple mt-auto">Aller au site</a>
                    </div>
                </div>
            </div>
        </div>
    </main>
</template>

<script>
</script>

<style scoped>
.bg-black {
    background-color: #000000;
}

.border-purple {
    border: 2px solid #bb4ed3;
    border-radius: 15px;
}

.text-purple {
    color: #c367d8;
}

.btn-purple {
    background-color: #bb4ed3;
    border-color: #bb4ed3;
    color: white;
    font-weight: 600;
    transition: all 0.3s ease;
}

.btn-purple:hover {
    background-color: #bb4ed3;
    border-color: #bb4ed3;
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(184, 72, 212, 0.3);
}

.card {
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    border-radius: 15px;
}

.card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 25px rgba(158, 47, 232, 0.4);
}

.card-img-top {
    border-radius: 10px;
    object-fit: contain;
}

header {
    text-align: center;
    background: linear-gradient(135deg, #8927a4 0%, #000000 100%);
}

.shadow-lg {
    box-shadow: 0 4px 15px rgba(111, 66, 193, 0.2);
}
</style>