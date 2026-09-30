<script lang="ts">
  import './catalogo.css';
  import { assetUrl } from '../../../../assets';
  import { onMount } from 'svelte';

  const originalScripts: { attributes: string[][]; content: string }[] = [];
  onMount(() => {
    const previousClass = document.body.className;
    const previousStyle = document.body.getAttribute('style');
    const titleElement = document.head.querySelector('title');
    const previousTitleId = titleElement?.getAttribute('id');
    
    
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
      
      
    };
  });
</script>

<section id="catalogo" class="fondo-principal">
  <div class="contenedor-seccion">
    <div class="catalogo-header">
      <span>Colección Exclusiva</span>
    
    
      <h2>Explora nuestros productos</h2>
    </div>

    <div style="display: flex; justify-content: flex-end; margin-bottom: 1.5rem; width: 100%;"><a href="catalogo.html" class="boton-catalogo" style="flex: 0 0 auto !important; width: auto !important; display: inline-flex; padding: 0.65rem 1rem;">Ver catálogo completo</a></div><div class="catalogo-contenido cuadricula">
      <div class="catalogo-item">
        <div class="catalogo-imagen">
          <img src={assetUrl("nova sound/imagenes/airpodspro01.jpg")} alt="Foto de AIRPORDS">
        </div>
        <div class="item-contenido">
          <div class="informacion-producto">
            <h3><a href="detalle.html?titulo=AIRPORDS&amp;precio=Precio%0A++++++++++++%0A++++++++++++%24250.000&amp;desc=vinculacion+inmediata+en+ecocistema+apple+y+cancelacion+de+ruido+ademas+icluye+funciones+inteligentes+como+el+audio+espacial+y+tiene+modo+ambiente+y+te+permite+escuchar+alrededor+sin+quitartelos+basta+con+abrir+el+estuche+para+se+vincule+automaticamentes&amp;img=%2Fnova+sound%2Fimagenes%2Fairpodspro01.jpg" style="color: inherit; text-decoration: none;">AIRPORDS</a></h3>
          </div>
          <p class="producto-descripcion">
            vinculacion inmediata en ecocistema apple y cancelacion de ruido ademas icluye funciones inteligentes como el audio espacial y tiene modo ambiente y te permite escuchar alrededor sin quitartelos basta con abrir el estuche para se vincule automaticamentes
          </p>
          <div class="precio">
            <span class="precio-label">Precio</span>
            <br>
            <span class="precio-valor">$250.000</span>
          </div>
        </div>
      </div>

      <div class="catalogo-item">
        <div class="catalogo-imagen">
          <img src={assetUrl("nova sound/imagenes/EARPODS-CONECTOR-TIPO-C.png")} alt="Foto de earpords">
        </div>
        <div class="item-contenido">
          <div class="informacion-producto">
            <h3><a href="detalle.html?titulo=earpords&amp;precio=Precio%0A++++++++++++%0A++++++++++++%24+0&amp;desc=se+destaca+por+confiabilidad+absoluta+sin+preocupacion+de+bateria+conexion+instantanea+y+calidad+de+microfono+superior+para+llamadasse+destaca+por+ser+comodo+y+duradero.&amp;img=%2Fnova+sound%2Fimagenes%2FEARPODS-CONECTOR-TIPO-C.png" style="color: inherit; text-decoration: none;">earpords</a></h3>
          </div>
          <p class="producto-descripcion">
            se destaca por confiabilidad absoluta sin preocupacion de bateria conexion instantanea y calidad de microfono superior para llamadasse destaca por ser comodo y duradero.
          </p>
          <div class="precio">
            <span class="precio-label">Precio</span>
            <br>
            <span class="precio-valor">$ 0</span>
          </div>
        </div>
      </div>

      <div class="catalogo-item">
        <div class="catalogo-imagen">
          <img src={assetUrl("nova sound/imagenes/images.jpg")} alt="Foto de powerbeats">
        </div>
        <div class="item-contenido">
          <div class="informacion-producto">
            <h3><a href="detalle.html?titulo=powerbeats&amp;precio=Precio%0A++++++++++++%0A++++++++++++%24300.000&amp;desc=audifonos+de+alto+rendimiento+con+un+dise%C3%B1o+ajustable+para+las+horas+a+diferenias+de+los+tactiles+tenemos+botones+para+evitar+accidentes+con+tacto+ofrecen+un+emparejamiento+instantaneo+con+ecocistemas+apple&amp;img=%2Fnova+sound%2Fimagenes%2Fimages.jpg" style="color: inherit; text-decoration: none;">powerbeats</a></h3>
          </div>
          <p class="producto-descripcion">
            audifonos de alto rendimiento con un diseño ajustable para las horas a diferenias de los tactiles tenemos botones para evitar accidentes con tacto ofrecen un emparejamiento instantaneo con ecocistemas apple
          </p>
          <div class="precio">
            <span class="precio-label">Precio</span>
            <br>
            <span class="precio-valor">$300.000</span>
          </div>
        </div>
      </div>
    </div>
    


  
  </div>
</section>