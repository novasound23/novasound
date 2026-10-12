<script lang="ts">
  import './navbar.css';
  import { onMount } from 'svelte';
  import { assetUrl } from '../../../../assets';
  export let scrolled = false;
  let scrollY = 0;
  let menuOpen = false;
  function closeMenu() { menuOpen = false; }
  onMount(() => {
    const previousOverflow = document.body.style.overflow;
    return () => { document.body.style.overflow = previousOverflow; };
  });
  $: if (typeof document !== 'undefined') document.body.style.overflow = menuOpen ? 'hidden' : '';

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
<svelte:window bind:scrollY on:click={closeMenu} />
<nav use:configureRoot={{ attributes: pageAttributes, links: pageLinks }} id="barra-navegacion" class="navbar" class:navbar-scrolled={scrolled || scrollY > 80}>
  <div class="contenedor-navbar">
    <a href="#heroe" class="navbar-logo">nova sound</a>
    
    <!-- Botón hamburguesa responsive para móviles -->
    <button class="navbar-toggle" id="navbar-toggle" aria-label="Abrir menú" aria-expanded={menuOpen} class:active={menuOpen} on:click|stopPropagation={() => menuOpen = !menuOpen}>
      <span></span>
      <span></span>
      <span></span>
    </button>
  
    <ul class="navbar-menu" class:active={menuOpen}>
      <li><a href="#heroe" class="nav-link">Inicio</a></li>
      <li><a href="#sobre-nosotros" class="nav-link">Sobre Nosotros</a></li>
      <li><a href="#catalogo" class="nav-link">Catálogo</a></li>
      <li><a href="#contacto" class="nav-link nav-link-btn">Contacto</a></li>
    </ul>
  </div>
</nav>