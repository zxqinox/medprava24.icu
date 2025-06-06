// DOM Elements
const header = document.querySelector('header');
const burger = document.querySelector('.burger');
const nav = document.querySelector('.nav-links');
const navLinks = document.querySelectorAll('.nav-links li');
const scrollTopButton = document.querySelector('.scroll-top');
const cookieConsent = document.querySelector('#cookie-consent');
const acceptCookiesButton = document.querySelector('#accept-cookies');
const preloader = document.querySelector('#preloader');
const contactDropdown = document.querySelector('.contact-dropdown');

// Preloader
window.addEventListener('load', () => {
    setTimeout(() => {
        preloader.style.display = 'none';
    }, 500);
});

// Mobile Navigation
burger.addEventListener('click', () => {
    nav.classList.toggle('active');
    burger.classList.toggle('active');
    
    // Animate Links
    navLinks.forEach((link, index) => {
        if (link.style.animation) {
            link.style.animation = '';
        } else {
            link.style.animation = `navLinkFade 0.5s ease forwards ${index / 7 + 0.3}s`;
        }
    });
});

// Mobile Contact Dropdown
if (window.innerWidth <= 768) {
    const dropdownButton = contactDropdown.querySelector('.contact-button');
    const dropdownContent = contactDropdown.querySelector('.contact-dropdown-content');
    
    dropdownButton.addEventListener('click', (e) => {
        e.preventDefault();
        dropdownContent.style.display = dropdownContent.style.display === 'block' ? 'none' : 'block';
    });
}

// Close dropdown when clicking outside
document.addEventListener('click', (e) => {
    if (!contactDropdown.contains(e.target) && window.innerWidth <= 768) {
        const dropdownContent = contactDropdown.querySelector('.contact-dropdown-content');
        dropdownContent.style.display = 'none';
    }
});

// Smooth Scrolling
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function (e) {
        e.preventDefault();
        const target = document.querySelector(this.getAttribute('href'));
        if (target) {
            target.scrollIntoView({
                behavior: 'smooth',
                block: 'start'
            });
            // Close mobile menu if open
            nav.classList.remove('active');
            burger.classList.remove('active');
        }
    });
});

// Scroll Events
window.addEventListener('scroll', () => {
    // Header Shadow
    if (window.scrollY > 50) {
        header.classList.add('scrolled');
    } else {
        header.classList.remove('scrolled');
    }

    // Scroll to Top Button
    if (window.scrollY > 500) {
        scrollTopButton.classList.add('visible');
    } else {
        scrollTopButton.classList.remove('visible');
    }

    // Active Navigation Link
    const sections = document.querySelectorAll('section');
    sections.forEach(section => {
        const sectionTop = section.offsetTop - 100;
        const sectionHeight = section.clientHeight;
        if (window.scrollY >= sectionTop && window.scrollY < sectionTop + sectionHeight) {
            const id = section.getAttribute('id');
            document.querySelectorAll('.nav-links a').forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('href') === `#${id}`) {
                    link.classList.add('active');
                }
            });
        }
    });
});

// Scroll to Top
scrollTopButton.addEventListener('click', () => {
    window.scrollTo({
        top: 0,
        behavior: 'smooth'
    });
});

// Cookie Consent
const checkCookieConsent = () => {
    if (!localStorage.getItem('cookieConsent')) {
        setTimeout(() => {
            cookieConsent.classList.add('show');
        }, 2000);
    }
};

acceptCookiesButton.addEventListener('click', () => {
    localStorage.setItem('cookieConsent', 'true');
    cookieConsent.classList.remove('show');
});

// Logo Upload
const logoUpload = document.getElementById('logo-upload');
const logoImage = document.getElementById('logo-image');
const footerLogoImage = document.getElementById('footer-logo-image');

logoUpload.addEventListener('change', function(e) {
    const file = e.target.files[0];
    if (file) {
        const reader = new FileReader();
        reader.onload = function(e) {
            logoImage.src = e.target.result;
            footerLogoImage.src = e.target.result;
            // Save to localStorage
            localStorage.setItem('customLogo', e.target.result);
        };
        reader.readAsDataURL(file);
    }
});

// Load custom logo if exists
const savedLogo = localStorage.getItem('customLogo');
if (savedLogo) {
    logoImage.src = savedLogo;
    footerLogoImage.src = savedLogo;
}

// Animations on Scroll
const handleScrollAnimations = () => {
    const elements = document.querySelectorAll('.service-card, .step, .document-item');
    
    elements.forEach(element => {
        const elementTop = element.getBoundingClientRect().top;
        const elementBottom = element.getBoundingClientRect().bottom;
        
        if (elementTop < window.innerHeight - 100 && elementBottom > 0) {
            element.style.opacity = '1';
            element.style.transform = 'translateY(0)';
        }
    });
};

// Initialize animations
document.addEventListener('DOMContentLoaded', () => {
    const elements = document.querySelectorAll('.service-card, .step, .document-item');
    elements.forEach(element => {
        element.style.opacity = '0';
        element.style.transform = 'translateY(20px)';
        element.style.transition = 'all 0.6s ease';
    });
    
    handleScrollAnimations();
});

window.addEventListener('scroll', handleScrollAnimations);

// Initialize
checkCookieConsent();

// Form Submission
const contactForm = document.querySelector('.contact-form');
if (contactForm) {
    contactForm.addEventListener('submit', function(e) {
        e.preventDefault();
        
        // Get form data
        const formData = new FormData(this);
        const formObject = {};
        formData.forEach((value, key) => {
            formObject[key] = value;
        });

        // Here you would typically send the form data to a server
        // For now, we'll just show a success message
        alert('Спасибо за ваше сообщение! Мы свяжемся с вами в ближайшее время.');
        this.reset();
    });
}

// Scroll Animation for Elements
const animateOnScroll = (elements, options = {}) => {
    const defaultOptions = {
        threshold: 0.2,
        rootMargin: '0px',
        animationClass: 'animate'
    };

    const finalOptions = { ...defaultOptions, ...options };

    const observer = new IntersectionObserver((entries, observer) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                entry.target.classList.add(finalOptions.animationClass);
                observer.unobserve(entry.target);
            }
        });
    }, {
        threshold: finalOptions.threshold,
        rootMargin: finalOptions.rootMargin
    });

    elements.forEach(el => observer.observe(el));
};

// Initialize animations for different sections
document.addEventListener('DOMContentLoaded', () => {
    // Service Cards Animation
    const serviceCards = document.querySelectorAll('.service-card');
    serviceCards.forEach(card => {
        card.style.opacity = '0';
        card.style.transform = 'translateY(30px)';
    });
    animateOnScroll(serviceCards, {
        animationClass: 'fade-in'
    });

    // Document Items Animation
    const documentItems = document.querySelectorAll('.document-item');
    documentItems.forEach(item => {
        item.style.opacity = '0';
        item.style.transform = 'translateY(30px)';
    });
    animateOnScroll(documentItems, {
        animationClass: 'fade-in'
    });

    // Contact Items Animation
    const contactItems = document.querySelectorAll('.contact-item');
    contactItems.forEach((item, index) => {
        item.style.opacity = '0';
        item.style.transform = 'translateX(-30px)';
        setTimeout(() => {
            item.style.transition = 'all 0.5s ease';
            item.style.opacity = '1';
            item.style.transform = 'translateX(0)';
        }, index * 200);
    });
});

// Add CSS animations
const style = document.createElement('style');
style.textContent = `
    @keyframes navLinkFade {
        from {
            opacity: 0;
            transform: translateX(50px);
        }
        to {
            opacity: 1;
            transform: translateX(0);
        }
    }

    .burger.toggle .line1 {
        transform: rotate(-45deg) translate(-5px, 6px);
    }

    .burger.toggle .line2 {
        opacity: 0;
    }

    .burger.toggle .line3 {
        transform: rotate(45deg) translate(-5px, -6px);
    }

    .fade-in {
        animation: fadeIn 0.6s ease-out forwards;
    }

    @keyframes fadeIn {
        from {
            opacity: 0;
            transform: translateY(30px);
        }
        to {
            opacity: 1;
            transform: translateY(0);
        }
    }
`;
document.head.appendChild(style);

// Parallax Effect for Hero Section
window.addEventListener('scroll', () => {
    const hero = document.querySelector('.hero');
    if (hero) {
        const scroll = window.pageYOffset;
        hero.style.backgroundPositionY = `${scroll * 0.5}px`;
    }
}); 
