<script lang="ts">
  import './heroe.css';
  import { assetUrl } from '../../../../assets';
  // Props o lógica del componente
</script>

<section class="heroe-seccion" id="heroe" aria-labelledby="heroe-titulo">
        <div class="heroe-contenedor">
          <div class="heroe-texto">
            <h1 id="heroe-titulo">Tu mundo,<span>tu sonido.</span></h1>
            <p class="heroe-descripcion">Encuentra los audífonos que van contigo. Comodidad, estilo y un gran sonido a un precio que se adapta a ti.</p>
            <div class="heroe-acciones">
              <a href="#catalogo" class="boton boton-secundario">Explorar catálogo <span aria-hidden="true">↗</span></a>
            </div>
            <p class="heroe-nota">Para tus playlists, tus llamadas y todo lo que mueve tu día.</p>
          </div>
          <figure class="heroe-imagen-contenedor">
            <img class="heroe-imagen" src={assetUrl("nova sound/imagenes/hero-imagen.png")} alt="Interior de Nova Sound con audífonos y equipos de audio" fetchpriority="high" decoding="async">
          </figure>
        </div>
      </section>
