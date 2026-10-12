<script lang="ts">
  import './catalogo.css';
  import productos from '../../data/productos.json';
  import { assetUrl } from '../../assets';
  import { onMount } from 'svelte';
  import Navbar from '../home/section/navbar/navbar.svelte';
  import Footer from '../home/section/footer/footer.svelte';
  onMount(() => {
    const previousClass = document.body.className;
    const previousStyle = document.body.getAttribute('style');
    document.body.className = 'pagina-catalogo-cuerpo';
    document.body.removeAttribute('style');
    return () => {
      document.body.className = previousClass;
      if (previousStyle === null) document.body.removeAttribute('style');
      else document.body.setAttribute('style', previousStyle);
    };
  });
</script>
<svelte:head><meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Explora nuestros productos • Catálogo Oficial</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="">
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&amp;family=Playfair+Display:ital,wght@0,500;0,600;0,700;1,400&amp;display=swap" rel="stylesheet"></svelte:head>


  <!-- 1. Header / Navbar Original del Proyecto (index.html) -->
<Navbar scrolled={true} pageLinks={["index.html#heroe","index.html#heroe","index.html#sobre-nosotros","index.html#catalogo","index.html#contacto"]} />

  <nav class="catalogo-miga-pan" aria-label="Navegación de migas de pan">
    <div class="catalogo-miga-contenedor">
      <ol class="catalogo-miga-lista">
        <li><a href={assetUrl('')}>Inicio</a></li>
        <li class="separador" aria-hidden="true">/</li>
        <li class="activo" aria-current="page">Catálogo</li>
      </ol>
    </div>
  </nav>
  <!-- 2. Área Principal del Catálogo -->
  <main class="seccion-catalogo-externa">
    <section id="catalogo">
      <div class="contenedor-seccion">
        <div class="catalogo-header">
          <span>Colección Exclusiva</span>
          <h2>Explora nuestros productos</h2>
          <p>Explora nuestra colección completa de artículos.</p>
        </div>
        <div class="catalogo-grid-wrapper">
          {#each productos as producto (producto.id)}
            <article class="card-overlay-hover">
              <div class="card-img-box">
                <img src={assetUrl(producto.imagen)} alt={producto.nombre} loading="lazy">
              </div>
              <div class="card-badge-flotante"><span>{producto.precio}</span></div>
              <div class="card-capa-hover">
                <h3>{producto.nombre}</h3>
                <span class="card-precio">{producto.precio}</span>
                <p>{producto.descripcion}</p>
                <a href={assetUrl('detalle/' + encodeURIComponent(producto.id))} class="card-boton-accion">
                  <span>Ver detalles</span>
                </a>
              </div>
            </article>
          {/each}
        </div>
      </div>
    </section>
  </main>

  <!-- 3. Footer Original del Proyecto (index.html) -->
<Footer pageAttributes={{"class":"sitio-footer","id":"pie-de-pagina"}} pageLinks={["index.html#heroe","index.html#sobre-nosotros","index.html#catalogo","index.html#contacto"]} />

  

