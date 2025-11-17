<template>
    <div class="page-container">

        <div class="section-header">
            <h3 class="lettreSommaire">Ici vous aurez de la mise en place de projet avec les explication pour pratiquer</h3>
        </div>

        <!-- =============================================================\\T//==================================================================== -->
        <div class="section-header">
            <h3 class="lettreSommaire">T</h3>
        </div>

         <div class="card border-purple shadow-lg">
            <div class="card-body bg-light-purple">
                <h5 class="card-title text-purple">Tests unitaire avec des mocks</h5>
                <p class="card-text">Crée des test unitaire a base de mock dans un projet</p>
                <NuxtLink class="btn btn-purple btn-hover mt-auto text-white text-decoration-none"
                    to="lessons/test_unitaire_mock">
                    Accès à la leçon
                </NuxtLink>
            </div>
        </div>

        <div class="card border-purple shadow-lg">
            <div class="card-body bg-light-purple">
                <h5 class="card-title text-purple">Tests unitaire dans un projet</h5>
                <p class="card-text">crée un projet et y intégrer des tests unitaire</p>
                <NuxtLink class="btn btn-purple btn-hover mt-auto text-white text-decoration-none"
                    to="lessons/test_unitaire">
                    Accès à la leçon
                </NuxtLink>
            </div>
        </div>


    </div>
</template>


<!-- =============================================================\\STYLE//==================================================================== -->
<style scoped>
.page-container {
    padding: 2rem;
    background: #f8f9fa;
}

.section-header {
    margin: 2rem 0 1rem 0;
}

.lettreSommaire {
    margin: 1vw;
    font-size: 2.5rem;
    font-weight: bold;
    color: #6A3093;
    text-align: center;
}

/* Classes CSS de l'autre page appliquées */
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
    text-decoration: none;
    display: inline-block;
    cursor: pointer;
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
    margin-bottom: 2rem;
}

.card:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 35px rgba(106, 48, 147, 0.15);
    border-color: #8B5FBF;
}

.shadow-lg {
    box-shadow: 0 4px 25px rgba(106, 48, 147, 0.1) !important;
}

.transition-all {
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
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

.card {
    animation: fadeInUp 0.6s ease forwards;
}

/* Responsive adjustments */
@media (max-width: 768px) {
    .card {
        margin-bottom: 1.5rem;
    }

    .page-container {
        padding: 1rem;
    }

    .lettreSommaire {
        font-size: 2rem;
    }
}

/* Styles pour les liens NuxtLink */
.text-white {
    color: white !important;
}

.text-decoration-none {
    text-decoration: none !important;
}
</style>