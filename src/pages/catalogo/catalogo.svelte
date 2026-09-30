<script lang="ts">
  import './catalogo.css';
  import { assetUrl } from '../../assets';
  import { onMount } from 'svelte';
  import Navbar from '../home/section/navbar/navbar.svelte';
  import Footer from '../home/section/footer/footer.svelte';
  const originalScripts: { attributes: string[][]; content: string }[] = [{"attributes":[],"content":"\n    // Garantiza que la barra de navegación mantenga su estado sólido al cargar\n    document.addEventListener('DOMContentLoaded', function() {\n      var headers = document.querySelectorAll('header, nav, .header, .navbar, #header, #navbar');\n      headers.forEach(function(h) {\n        h.classList.add('scrolled', 'header-scrolled', 'navbar-scrolled', 'activo', 'active');\n      });\n    });\n  "}];
  onMount(() => {
    const previousClass = document.body.className;
    const previousStyle = document.body.getAttribute('style');
    const titleElement = document.head.querySelector('title');
    const previousTitleId = titleElement?.getAttribute('id');
    
    document.body.className = "pagina-catalogo-cuerpo";
    document.body.setAttribute('style', "");
    const mountedScripts: HTMLScriptElement[] = [];
    let cancelled = false;
    // Re-run the original page scripts after Svelte mounts their original DOM.
    queueMicrotask(async () => {
      for (const original of originalScripts) {
        if (cancelled) break;
        const script = document.createElement('script');
        for (const [name, value] of original.attributes) {
          script.setAttribute(name, name === 'src' ? assetUrl(value) : value);
        }
        script.textContent = original.content.replace(/\b(?:window\.)?location\.search\b/g, '(window.__svelteProductSearch ?? window.location.search)');
        const loaded = script.src ? new Promise<void>((resolve) => {
          script.onload = () => resolve();
          script.onerror = () => resolve();
        }) : Promise.resolve();
        mountedScripts.push(script);
        document.body.appendChild(script);
        await loaded;
      }
    });
    return () => {
      cancelled = true;
      mountedScripts.forEach((script) => script.remove());
      
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
<Navbar pageAttributes={{"id":"barra-navegacion","class":"navbar scrolled header-scrolled navbar-scrolled activo active"}} pageLinks={["index.html#heroe","index.html#heroe","index.html#sobre-nosotros","index.html#catalogo","index.html#contacto"]} />

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
        <!-- Tarjeta: AIRPORDS -->
        <div class="card-overlay-hover">
          <div class="card-img-box">
            <img src={assetUrl("nova sound/imagenes/airpodspro01.jpg")} alt="Foto de AIRPORDS" loading="lazy" onerror="this.onerror=null;this.src='https://images.unsplash.com/photo-1522335789203-aabd1fc54bc9?w=800&amp;auto=format&amp;fit=crop&amp;q=80';">
          </div>
          <div class="card-badge-flotante">
            <span>$250.000</span>
          </div>
          <div class="card-capa-hover">
            <h3>AIRPORDS</h3>
            <span class="card-precio">$250.000</span>
            <p>vinculacion inmediata en ecocistema apple y cancelacion de ruido ademas icluye funciones inteligentes como el audio espacial y tiene modo ambiente y te permite escuchar alrededor sin quitartelos basta con abrir el estuche para se vincule automaticamentes</p>
            <a href="detalle.html?titulo=AIRPORDS&amp;precio=%24250.000&amp;img=.%2Fimagenes%2Fairpodspro01.jpg&amp;desc=vinculacion%20inmediata%20en%20ecocistema%20apple%20y%20cancelacion%20de%20ruido%20ademas%20icluye%20funciones%20inteligentes%20como%20el%20audio%20espacial%20y%20tiene%20modo%20ambiente%20y%20te%20permite%20escuchar%20alrededor%20sin%20quitartelos%20basta%20con%20abrir%20el%20estuche%20para%20se%20vincule%20automaticamentes" class="card-boton-accion">
              <span>Ver detalles</span>
            </a>
          </div>
        </div>

        <!-- Tarjeta: earpords -->
        <div class="card-overlay-hover">
          <div class="card-img-box">
            <img src={assetUrl("nova sound/imagenes/EARPODS-CONECTOR-TIPO-C.png")} alt="Foto de earpords" loading="lazy" onerror="this.onerror=null;this.src='https://images.unsplash.com/photo-1596462502278-27bfdc403348?w=800&amp;auto=format&amp;fit=crop&amp;q=80';">
          </div>
          <div class="card-badge-flotante">
            <span>$ 0</span>
          </div>
          <div class="card-capa-hover">
            <h3>earpords</h3>
            <span class="card-precio">$ 0</span>
            <p>se destaca por confiabilidad absoluta sin preocupacion de bateria conexion instantanea y calidad de microfono superior para llamadasse destaca por ser comodo y duradero.</p>
            <a href="detalle.html?titulo=earpords&amp;precio=%24%200&amp;img=.%2Fimagenes%2FEARPODS-CONECTOR-TIPO-C.png&amp;desc=se%20destaca%20por%20confiabilidad%20absoluta%20sin%20preocupacion%20de%20bateria%20conexion%20instantanea%20y%20calidad%20de%20microfono%20superior%20para%20llamadasse%20destaca%20por%20ser%20comodo%20y%20duradero." class="card-boton-accion">
              <span>Ver detalles</span>
            </a>
          </div>
        </div>

        <!-- Tarjeta: powerbeats -->
        <div class="card-overlay-hover">
          <div class="card-img-box">
            <img src={assetUrl("nova sound/imagenes/images.jpg")} alt="Foto de powerbeats" loading="lazy" onerror="this.onerror=null;this.src='https://images.unsplash.com/photo-1556911220-e15b29be8c8f?w=800&amp;auto=format&amp;fit=crop&amp;q=80';">
          </div>
          <div class="card-badge-flotante">
            <span>$300.000</span>
          </div>
          <div class="card-capa-hover">
            <h3>powerbeats</h3>
            <span class="card-precio">$300.000</span>
            <p>audifonos de alto rendimiento con un diseño ajustable para las horas a diferenias de los tactiles tenemos botones para evitar accidentes con tacto ofrecen un emparejamiento instantaneo con ecocistemas apple</p>
            <a href="detalle.html?titulo=powerbeats&amp;precio=%24300.000&amp;img=.%2Fimagenes%2Fimages.jpg&amp;desc=audifonos%20de%20alto%20rendimiento%20con%20un%20dise%C3%B1o%20ajustable%20para%20las%20horas%20a%20diferenias%20de%20los%20tactiles%20tenemos%20botones%20para%20evitar%20accidentes%20con%20tacto%20ofrecen%20un%20emparejamiento%20instantaneo%20con%20ecocistemas%20apple" class="card-boton-accion">
              <span>Ver detalles</span>
            </a>
          </div>
        </div>
        </div>
      </div>
    </section>
  </main>

  <!-- 3. Footer Original del Proyecto (index.html) -->
<Footer pageAttributes={{"class":"sitio-footer","id":"pie-de-pagina"}} pageLinks={["index.html#heroe","index.html#sobre-nosotros","index.html#catalogo","index.html#contacto"]} />

  

