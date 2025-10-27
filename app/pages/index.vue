<template class="h-100">
    <header class="bg-gradient-primary text-white py-5 mb-4">
        <div class="container">
            <h1 class="display-4 fw-bold mb-3">Bienvenue sur le recueil de cours</h1>
            <h4 class="fw-light opacity-75">Ma plateforme d'apprentissage des technologies web</h4>
        </div>
    </header>

    <main class="container-fluid bg-light min-vh-100 py-5">
        <div class="row justify-content-center g-4">
            <div class="col-md-4 col-lg-3">
                <div class="card bg-white border-purple shadow-lg h-100 transition-all m-3">
                    <div class="card-img-container p-4 bg-light-purple">
                        <img class="card-img" src="/img_index/php.png" alt="Logo PHP">
                    </div>
                    <div class="card-body d-flex flex-column">
                        <h5 class="card-title text-purple fw-bold fs-4">La doc officielle de PHP</h5>
                        <p class="card-text text-dark flex-grow-1">Toute la doc officielle de PHP si jamais les exemples présents sur le recueil ne suffisent pas !</p>
                        <a href="https://www.php.net/docs.php" target="_blank" class="btn btn-purple btn-hover mt-auto">Aller au site</a>
                    </div>
                </div>
            </div>
            
            <div class="col-md-4 col-lg-3">
                <div class="card bg-white border-purple shadow-lg h-100 transition-all m-3">
                    <div class="card-img-container p-4 bg-light-purple">
                        <img class="card-img" src="/img_index/js.png" alt="Logo JavaScript">
                    </div>
                    <div class="card-body d-flex flex-column">
                        <h5 class="card-title text-purple fw-bold fs-4">La doc de JavaScript</h5>
                        <p class="card-text text-dark flex-grow-1">Ici se trouve la doc de JavaScript</p>
                        <a href="https://jsdoc.app/" target="_blank" class="btn btn-purple btn-hover mt-auto">Aller au site</a>
                    </div>
                </div>
            </div>

            <div class="col-md-4 col-lg-3">
                <div class="card bg-white border-purple shadow-lg h-100 transition-all m-3">
                    <div class="card-img-container p-4 bg-light-purple">
                        <img class="card-img" src="/img_index/sql.png" alt="Logo sql">
                    </div>
                    <div class="card-body d-flex flex-column">
                        <h5 class="card-title text-purple fw-bold fs-4">La doc SQL</h5>
                        <p class="card-text text-dark flex-grow-1">Ici se trouve la doc de SQL</p>
                        <a href="https://sql.sh/" target="_blank" class="btn btn-purple btn-hover mt-auto">Aller au site</a>
                    </div>
                </div>
            </div>
            
            <div class="col-md-4 col-lg-3">
                <div class="card bg-white border-purple shadow-lg h-100 transition-all m-3">
                    <div class="card-img-container p-4 bg-light-purple">
                        <img class="card-img" src="/img_index/java.png" alt="Logo Java">
                    </div>
                    <div class="card-body d-flex flex-column">
                        <h5 class="card-title text-purple fw-bold fs-4">Java</h5>
                        <p class="card-text text-dark flex-grow-1">La doc officielle de Java</p>
                        <a href="#" target="_blank" class="btn btn-purple btn-hover mt-auto">Aller au site</a>
                    </div>
                </div>
            </div>

            <div class="col-md-4 col-lg-3">
                <div class="card bg-white border-purple shadow-lg h-100 transition-all m-3">
                    <div class="card-img-container p-4 bg-light-purple">
                        <img class="card-img" src="/img_index/grafikart.png" alt="Logo grafikart">
                    </div>
                    <div class="card-body d-flex flex-column">
                        <h5 class="card-title text-purple fw-bold fs-4">Grafikart.fr</h5>
                        <p class="card-text text-dark flex-grow-1">Le site de grafikart regroupe des leçons et astuces de manière très pédagogique sur beaucoup de langages, ce site est une référence dans le monde du dev.</p>
                        <a href="https://grafikart.fr/" target="_blank" class="btn btn-purple btn-hover mt-auto">Aller au site</a>
                    </div>
                </div>
            </div>

        </div>
    </main>
</template>

<script>

</script>

<style scoped>
.bg-gradient-primary {
    background: linear-gradient(135deg, #8B5FBF 0%, #6A3093 100%);
}

.bg-light-purple {
    background-color: #f8f6ff;
    border-radius: 12px 12px 0 0;
}

.border-purple {
    border: 2px solid #e0d6ff;
    border-radius: 15px;
    transition: all 0.3s ease;
}

.text-purple {
    color: #6A3093 !important;
}

.btn-purple {
    background: linear-gradient(135deg, #8B5FBF 0%, #6A3093 100%);
    border: none;
    color: white;
    font-weight: 600;
    padding: 12px 24px;
    border-radius: 8px;
    transition: all 0.3s ease;
    box-shadow: 0 4px 15px rgba(106, 48, 147, 0.2);
}

.btn-purple:hover {
    background: linear-gradient(135deg, #7a4fa8 0%, #5a287a 100%);
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(106, 48, 147, 0.3);
    color: white;
}

.btn-hover {
    position: relative;
    overflow: hidden;
}

.btn-hover::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    width: 0;
    height: 0;
    background: rgba(255, 255, 255, 0.2);
    border-radius: 50%;
    transition: all 0.5s ease;
    transform: translate(-50%, -50%);
}

.btn-hover:hover::after {
    width: 300px;
    height: 300px;
}

.card {
    transition: all 0.3s ease;
    border-radius: 15px;
    overflow: hidden;
}

.card:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 35px rgba(106, 48, 147, 0.15);
    border-color: #8B5FBF;
}

.card-img {
    height: auto;
    object-fit: contain;
    transition: transform 0.3s ease;
}

.card:hover .card-img {
    transform: scale(1.05);
}

.card-img-container {
    transition: all 0.3s ease;
}

.card:hover .card-img-container {
    background: linear-gradient(135deg, #f0ebff 0%, #e0d6ff 100%);
}

.shadow-lg {
    box-shadow: 0 4px 25px rgba(106, 48, 147, 0.1) !important;
}

.transition-all {
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

header {
    background: linear-gradient(135deg, #8B5FBF 0%, #6A3093 100%);
    position: relative;
    overflow: hidden;
}

header::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: url("data:image/svg+xml,%3Csvg width='100' height='100' viewBox='0 0 100 100' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M11 18c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm48 25c3.866 0 7-3.134 7-7s-3.134-7-7-7-7 3.134-7 7 3.134 7 7 7zm-43-7c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm63 31c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM34 90c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zm56-76c1.657 0 3-1.343 3-3s-1.343-3-3-3-3 1.343-3 3 1.343 3 3 3zM12 86c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm28-65c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm23-11c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-6 60c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm29 22c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zM32 63c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm57-13c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5zm-9-21c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM60 91c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM35 41c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2zM12 60c1.105 0 2-.895 2-2s-.895-2-2-2-2 .895-2 2 .895 2 2 2z' fill='%23ffffff' fill-opacity='0.03' fill-rule='evenodd'/%3E%3C/svg%3E");
}

/* Responsive adjustments */
@media (max-width: 768px) {
    .card {
        margin-bottom: 1.5rem;
    }
    
    header h1 {
        font-size: 2rem;
    }
    
    header h4 {
        font-size: 1.1rem;
    }
}

/* Animation d'entrée pour les cartes */
@keyframes fadeInUp {
    from {
        opacity: 0;
        transform: translateY(30px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

.col-md-4 {
    animation: fadeInUp 0.6s ease forwards;
}

.col-md-4:nth-child(1) { animation-delay: 0.1s; }
.col-md-4:nth-child(2) { animation-delay: 0.2s; }
.col-md-4:nth-child(3) { animation-delay: 0.3s; }
.col-md-4:nth-child(4) { animation-delay: 0.4s; }
</style>