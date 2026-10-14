<script lang="ts">
  import './navbar.css';
  import { onMount } from 'svelte';
  let abierto = false;
  export let scrolled = false;
  let navbar: HTMLElement;
  let overflowAnterior = '';

  function cerrarMenu() {
    if (!abierto) return;
    abierto = false;
    document.body.style.overflow = overflowAnterior;
  }

  function alternarMenu() {
    if (abierto) cerrarMenu();
    else {
      overflowAnterior = document.body.style.overflow;
      abierto = true;
      document.body.style.overflow = 'hidden';
    }
  }

  onMount(() => {
    const actualizarScroll = () => { scrolled = window.scrollY > 80; };
    const cerrarAlNavegar = (event: MouseEvent) => {
      const target = event.target;
      if (target instanceof Element && (!navbar.contains(target) || target.closest('a'))) cerrarMenu();
    };
    const cerrarConEscape = (event: KeyboardEvent) => { if (event.key === 'Escape') cerrarMenu(); };
    const ajustarPantalla = () => { if (window.innerWidth > 768) cerrarMenu(); };
    actualizarScroll();
    window.addEventListener('scroll', actualizarScroll, { passive: true });
    window.addEventListener('click', cerrarAlNavegar, true);
    window.addEventListener('keydown', cerrarConEscape);
    window.addEventListener('resize', ajustarPantalla);
    return () => {
      cerrarMenu();
      window.removeEventListener('scroll', actualizarScroll);
      window.removeEventListener('click', cerrarAlNavegar, true);
      window.removeEventListener('keydown', cerrarConEscape);
      window.removeEventListener('resize', ajustarPantalla);
    };
  });
  export let pageAttributes: Record<string, string> = {};
  export let pageLinks: string[] = [];
  function configureRoot(node: HTMLElement, config: { attributes: Record<string, string>; links: string[] }) {
    const update = (value: typeof config) => {
      Object.entries(value.attributes).forEach(([name, content]) => node.setAttribute(name, content));
      node.querySelectorAll('a').forEach((link, index) => {
        if (value.links[index] !== undefined) link.setAttribute('href', value.links[index]);
      });
    };
    update(config);
    return { update };
  }
</script>
<nav bind:this={navbar} use:configureRoot={{ attributes: pageAttributes, links: pageLinks }} id="barra-navegacion" class="navbar" class:navbar-scrolled={scrolled}>
      <div class="contenedor-navbar">
        <a href="#heroe" class="navbar-logo">Nova Sound</a>

        <!-- Botón hamburguesa responsive para móviles -->
        <button type="button" class="navbar-toggle" class:active={abierto} id="navbar-toggle" aria-label={abierto ? 'Cerrar menú' : 'Abrir menú'} aria-expanded={abierto} aria-controls="navbar-menu" on:click={alternarMenu}>
          <span></span>
          <span></span>
          <span></span>
        </button>

        <ul class="navbar-menu" id="navbar-menu" class:active={abierto}>
          <li><a href="#heroe" class="nav-link">Inicio</a></li>
          <li><a href="#sobre-nosotros" class="nav-link">Sobre Nosotros</a></li>
          <li><a href="#catalogo" class="nav-link">Catálogo</a></li>
          <li>
            <a href="#contacto" class="nav-link nav-link-btn">Contacto</a>
          </li>
        </ul>
      </div>
    </nav>
