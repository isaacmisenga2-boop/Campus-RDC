
/* CAMPUS RDC - Application V1.0 */

document.addEventListener("DOMContentLoaded", () => {
  const $ = (selector) => document.querySelector(selector);
  const $$ = (selector) => [...document.querySelectorAll(selector)];

  // NAVIGATION
  const navLinks = $$("[data-section], .nav-link, [data-page]");
  const sections = $$(".app-section, .page-section, section[id]");

  function showSection(target) {
    if (!target) return;

    sections.forEach((section) => {
      section.hidden = section.id !== target;
      section.classList.toggle("active", section.id === target);
    });

    navLinks.forEach((link) => {
      const id = link.dataset.section || link.dataset.page;
      link.classList.toggle("active", id === target);
    });
  }

  navLinks.forEach((link) => {
    link.addEventListener("click", (event) => {
      const target = link.dataset.section || link.dataset.page;

      if (target) {
        event.preventDefault();
        showSection(target);
      }
    });
  });

  // RECHERCHE DES COURS
  const searchInput = $(
    "#courseSearch, #searchInput, [data-course-search]"
  );

  if (searchInput) {
    searchInput.addEventListener("input", () => {
      const term = searchInput.value.trim().toLocaleLowerCase();

      $$(".course-card, [data-course]").forEach((card) => {
        card.hidden = !card.textContent
          .toLocaleLowerCase()
          .includes(term);
      });
    });
  }

  // PROFIL ETUDIANT
  const profileForm = $("#profileForm, [data-profile-form]");

  const nameInput = $(
    "#studentName, #profileName, [name='studentName']"
  );

  const universityInput = $(
    "#studentUniversity, #university, [name='university']"
  );

  const facultyInput = $(
    "#studentFaculty, #faculty, [name='faculty']"
  );

  const profileMessage = $(
    "#profileMessage, [data-profile-message]"
  );

  // CHARGER LE PROFIL
  try {
    const saved = JSON.parse(
      localStorage.getItem("campusRdcProfile") || "{}"
    );

    if (nameInput && saved.name) {
      nameInput.value = saved.name;
    }

    if (universityInput && saved.university) {
      universityInput.value = saved.university;
    }

    if (facultyInput && saved.faculty) {
      facultyInput.value = saved.faculty;
    }
  } catch (error) {
    console.log("Profil non disponible.");
  }

  // ENREGISTRER LE PROFIL
  if (profileForm) {
    profileForm.addEventListener("submit", (event) => {
      event.preventDefault();

      const profile = {
        name: nameInput?.value.trim() || "",
        university: universityInput?.value.trim() || "",
        faculty: facultyInput?.value.trim() || ""
      };

      try {
        localStorage.setItem(
          "campusRdcProfile",
          JSON.stringify(profile)
        );

        if (profileMessage) {
          profileMessage.textContent =
            "Profil enregistré sur cet appareil.";
        }

        const displayedName = $(
          "#displayStudentName, [data-display-name]"
        );

        if (displayedName) {
          displayedName.textContent =
            profile.name || "Étudiant";
        }

      } catch (error) {
        if (profileMessage) {
          profileMessage.textContent =
            "Enregistrement indisponible.";
        }
      }
    });
  }

  // AFFICHER LE NOM
  try {
    const profile = JSON.parse(
      localStorage.getItem("campusRdcProfile") || "{}"
    );

    const displayedName = $(
      "#displayStudentName, [data-display-name]"
    );

    if (displayedName && profile.name) {
      displayedName.textContent = profile.name;
    }
  } catch (error) {
    console.log("Aucun profil enregistré.");
  }

  // MENU MOBILE
  const menuButton = $(
    "#menuToggle, [data-menu-toggle]"
  );

  const menu = $(
    "#mainNav, .main-nav, [data-main-nav]"
  );

  if (menuButton && menu) {
    menuButton.addEventListener("click", () => {
      const expanded =
        menuButton.getAttribute("aria-expanded") === "true";

      menuButton.setAttribute(
        "aria-expanded",
        String(!expanded)
      );

      menu.classList.toggle("open", !expanded);
    });
  }

  // ANNEE AUTOMATIQUE
  const year = $(
    "#currentYear, [data-current-year]"
  );

  if (year) {
    year.textContent = new Date().getFullYear();
  }

  console.log("CAMPUS RDC est prêt !");
});
        
