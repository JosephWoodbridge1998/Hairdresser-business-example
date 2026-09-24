// ==========================================================================
// Example Business — script.js
// Handles: sticky header shrink, mobile nav, smooth scroll, booking form
// ==========================================================================

document.addEventListener('DOMContentLoaded', () => {

  /* ---------- Footer year ---------- */
  document.getElementById('year').textContent = new Date().getFullYear();

  /* ---------- Sticky header shrink on scroll ---------- */
  const header = document.getElementById('siteHeader');
  const onScroll = () => header.classList.toggle('scrolled', window.scrollY > 12);
  window.addEventListener('scroll', onScroll);
  onScroll();

  /* ---------- Mobile menu (hamburger) ---------- */
  const burger = document.getElementById('burgerBtn');
  const navLinks = document.getElementById('navLinks');

  function closeMenu() {
    navLinks.classList.remove('open');
    burger.classList.remove('open');
    burger.setAttribute('aria-expanded', 'false');
  }
  function toggleMenu() {
    const isOpen = navLinks.classList.toggle('open');
    burger.classList.toggle('open', isOpen);
    burger.setAttribute('aria-expanded', String(isOpen));
  }
  burger.addEventListener('click', toggleMenu);

  // Close mobile menu whenever a nav link is tapped
  navLinks.querySelectorAll('a').forEach(link => {
    link.addEventListener('click', closeMenu);
  });

  /* ---------- Smooth scroll for all in-page anchor links ---------- */
  document.querySelectorAll('a[href^="#"]').forEach(link => {
    link.addEventListener('click', (e) => {
      const targetId = link.getAttribute('href');
      const target = document.querySelector(targetId);
      if (target) {
        e.preventDefault();
        const headerHeight = header.offsetHeight;
        const top = target.getBoundingClientRect().top + window.scrollY - headerHeight + 1;
        window.scrollTo({ top, behavior: 'smooth' });
      }
    });
  });

  /* ---------- Booking form ---------- */
  const form = document.getElementById('bookingForm');
  const confirmation = document.getElementById('formConfirmation');
  const waConfirmLink = document.getElementById('waConfirmLink');
  const WHATSAPP_NUMBER = '447400000000'; // Example Business placeholder number

  const requiredFields = ['bkName', 'bkEmail', 'bkPhone', 'bkService', 'bkDate', 'bkTime'];

  function validateField(id) {
    const field = document.getElementById(id);
    const group = field.closest('.form-group');
    let valid = field.value.trim() !== '';

    // Extra check for email format
    if (id === 'bkEmail' && valid) {
      valid = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(field.value.trim());
    }

    group.classList.toggle('invalid', !valid);
    return valid;
  }

  // Clear the error state as soon as the person starts fixing a field
  requiredFields.forEach(id => {
    const field = document.getElementById(id);
    field.addEventListener('input', () => validateField(id));
    field.addEventListener('change', () => validateField(id));
  });

  form.addEventListener('submit', (e) => {
    e.preventDefault();

    // Validate all required fields; collect overall pass/fail
    const results = requiredFields.map(validateField);
    const allValid = results.every(Boolean);

    if (!allValid) {
      // Scroll to first invalid field for a clear, friendly nudge
      const firstInvalid = form.querySelector('.form-group.invalid input, .form-group.invalid select');
      if (firstInvalid) firstInvalid.focus();
      return;
    }

    // Gather values
    const data = {
      name: document.getElementById('bkName').value.trim(),
      email: document.getElementById('bkEmail').value.trim(),
      phone: document.getElementById('bkPhone').value.trim(),
      service: document.getElementById('bkService').value,
      date: document.getElementById('bkDate').value,
      time: document.getElementById('bkTime').value,
      notes: document.getElementById('bkNotes').value.trim()
    };

    // Build a pre-filled WhatsApp message
    const message =
      `Hi Example Business! I'd like to book an appointment.%0A%0A` +
      `Name: ${encodeURIComponent(data.name)}%0A` +
      `Service: ${encodeURIComponent(data.service)}%0A` +
      `Preferred date: ${encodeURIComponent(data.date)}%0A` +
      `Preferred time: ${encodeURIComponent(data.time)}%0A` +
      (data.notes ? `Notes: ${encodeURIComponent(data.notes)}%0A` : '') +
      `%0AMy phone: ${encodeURIComponent(data.phone)}, email: ${encodeURIComponent(data.email)}`;

    waConfirmLink.href = `https://wa.me/${WHATSAPP_NUMBER}?text=${message}`;

    // Show a friendly confirmation instead of actually submitting anywhere
    // (there's no backend in this demo — wire this up to your booking system / email service)
    confirmation.classList.add('show');
    confirmation.scrollIntoView({ behavior: 'smooth', block: 'nearest' });

    form.reset();
  });

});
