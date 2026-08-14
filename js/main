/* =====================================================
   JSG - JAVASCRIPT
===================================================== */

let currentStep = 1;

let selectedProfile = "";

let selectedInterests = [];

let stars = 7340;


/* =====================================================
   ONBOARDING
===================================================== */

function nextStep(step) {

    document
        .querySelectorAll(".onboarding-screen")
        .forEach(screen => {
            screen.classList.remove("active");
        });

    const nextScreen = document.getElementById(`step${step}`);

    if (nextScreen) {

        nextScreen.classList.add("active");

        currentStep = step;

    }

}


/* =====================================================
   PROFILE
===================================================== */

function selectProfile(profile, element) {

    selectedProfile = profile;

    document
        .querySelectorAll(".profile-card")
        .forEach(card => {
            card.classList.remove("selected");
        });

    element.classList.add("selected");

    const button = document.getElementById("profileContinue");

    button.classList.remove("disabled");

}


/* =====================================================
   INTERESTS
===================================================== */

function toggleInterest(element) {

    const interest = element.textContent;

    element.classList.toggle("selected");

    if (selectedInterests.includes(interest)) {

        selectedInterests =
            selectedInterests.filter(
                item => item !== interest
            );

    } else {

        selectedInterests.push(interest);

    }

    updateInterestButton();

}


function updateInterestButton() {

    const button =
        document.getElementById("interestContinue");

    button.textContent =
        `Continuar (${selectedInterests.length}/3) →`;

    if (selectedInterests.length >= 3) {

        button.classList.remove("disabled");

    } else {

        button.classList.add("disabled");

    }

}


/* =====================================================
   FINISH ONBOARDING
===================================================== */

function finishOnboarding() {

    const name =
        document.getElementById("explorerName").value.trim();

    if (!name) {

        showToast("✏️ Escribe tu nombre de explorador");

        return;

    }

    localStorage.setItem(
        "jsgName",
        name
    );

    localStorage.setItem(
        "jsgProfile",
        selectedProfile
    );

    localStorage.setItem(
        "jsgInterests",
        JSON.stringify(selectedInterests)
    );

    document
        .getElementById("onboarding")
        .classList.add("hidden");

    document
        .getElementById("app")
        .classList.remove("hidden");

    loadUser();

    showToast(
        `🚀 ¡Bienvenido a JSG, ${name}!`
    );

}


/* =====================================================
   LOAD USER
===================================================== */

function loadUser() {

    const savedName =
        localStorage.getItem("jsgName");

    if (!savedName) return;

    document
        .getElementById("sidebarName")
        .textContent = savedName;

    document
        .getElementById("profileName")
        .textContent = savedName;

}


/* =====================================================
   NAVIGATION
===================================================== */

function showPage(page, element = null) {

    document
        .querySelectorAll(".page")
        .forEach(p => {
            p.classList.remove("active-page");
        });

    const target =
        document.getElementById(`page-${page}`);

    if (target) {

        target.classList.add("active-page");

    }


    document
        .querySelectorAll(".nav-item")
        .forEach(item => {
            item.classList.remove("active");
        });

    if (element) {

        element.classList.add("active");

    } else {

        const navItem =
            document.querySelector(
                `.nav-item[onclick*="'${page}'"]`
            );

        if (navItem) {

            navItem.classList.add("active");

        }

    }

}


/* =====================================================
   COURSE
===================================================== */

function enrollCourse(button) {

    button.textContent = "✓ Inscrito";

    button.style.background = "#28b779";

    addStars(50);

    showToast(
        "📚 ¡Te inscribiste al curso! +50 ⭐"
    );

}


function continueCourse(button) {

    button.textContent = "▶ Continuar 60%";

    addStars(30);

    showToast(
        "🚀 ¡Progreso actualizado! +30 ⭐"
    );

}


/* =====================================================
   STARS
===================================================== */

function addStars(amount) {

    stars += amount;

    updateStars();

}


function updateStars() {

    const formatted =
        stars.toLocaleString("es-PE");

    document
        .getElementById("starsCounter")
        .textContent = formatted;

    document
        .getElementById("sidebarStars")
        .textContent = formatted;

    document
        .getElementById("profileStars")
        .textContent = formatted;

}


/* =====================================================
   STORE
===================================================== */

function buyItem(price) {

    if (stars < price) {

        showToast(
            "😅 No tienes suficientes Stars"
        );

        return;

    }

    stars -= price;

    updateStars();

    showToast(
        `🎉 ¡Objeto comprado! -${price} ⭐`
    );

}


/* =====================================================
   COMMUNITY
===================================================== */

function createPost() {

    const input =
        document.getElementById("postInput");

    const text =
        input.value.trim();

    if (!text) {

        showToast(
            "✏️ Escribe algo antes de publicar"
        );

        return;

    }

    const posts =
        document.getElementById("posts");

    const article =
        document.createElement("article");

    article.className = "post";

    article.innerHTML = `

        <div class="post-user">

            🦙

            <strong>
                ${escapeHTML(
                    localStorage.getItem("jsgName")
                    || "Explorador"
                )}
            </strong>

            <span>
                ahora
            </span>

        </div>

        <p>
            ${escapeHTML(text)}
        </p>

        <div class="post-actions">

            ❤️ 0
            💬 0
            ⭐ 0

        </div>

    `;

    posts.prepend(article);

    input.value = "";

    addStars(10);

    showToast(
        "✨ Publicación creada +10 ⭐"
    );

}


/* =====================================================
   SECURITY
===================================================== */

function escapeHTML(text) {

    const div =
        document.createElement("div");

    div.textContent = text;

    return div.innerHTML;

}


/* =====================================================
   TOAST
===================================================== */

function showToast(message) {

    const toast =
        document.getElementById("toast");

    toast.textContent = message;

    toast.classList.add("show");

    setTimeout(() => {

        toast.classList.remove("show");

    }, 2500);

}


/* =====================================================
   START
===================================================== */

document.addEventListener(
    "DOMContentLoaded",
    () => {

        const savedName =
            localStorage.getItem("jsgName");

        /*
         * Si el usuario ya había completado
         * el onboarding, mostramos directamente
         * la aplicación.
         */

        if (savedName) {

            document
                .getElementById("onboarding")
                .classList.add("hidden");

            document
                .getElementById("app")
                .classList.remove("hidden");

            loadUser();

        }

        updateStars();

    }
);
