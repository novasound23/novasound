<script lang="ts">
  import './catalogo.css';
  import { assetUrl } from '../../../../assets';

  import productos from '../../../../data/productos.json';

  const productosAleatorios = [...productos];
  for (let i = productosAleatorios.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [productosAleatorios[i], productosAleatorios[j]] = [productosAleatorios[j], productosAleatorios[i]];
  }
  const productosHome = productosAleatorios.slice(0, 3);


</script>

<section id="catalogo" class="fondo-principal catalogo-home">
          <div class="contenedor-seccion">
            <div class="catalogo-header">
              <span>Colección Exclusiva</span>

              <h2>Explora nuestros productos</h2>
            </div>

            <div style="display: flex; justify-content: flex-end; margin-bottom: 1.5rem; width: 100%;"><a href="catalogo.html" class="boton-catalogo" style="flex: 0 0 auto !important; width: auto !important; display: inline-flex; padding: 0.65rem 1rem;">Ver catálogo completo</a></div><div class="catalogo-contenido cuadricula">
              {#each productosHome as producto (producto.id)}
<div class="catalogo-item" data-producto={producto.id}>
                <div class="catalogo-imagen">
                  <img src={assetUrl(producto.imagen)} alt={producto.nombre}>
                </div>
                <div class="item-contenido">
                  <div class="informacion-producto">
                    <h3><a href={assetUrl(`detalle/${encodeURIComponent(producto.id)}`)} style="color: inherit; text-decoration: none;">{producto.nombre}</a></h3>
                  </div>
                  <p class="producto-descripcion">{producto.descripcion}</p>
                  <div class="precio">
                    <span class="precio-label">Precio</span>
                    <br>
                    <span class="precio-valor">{producto.precio}</span>
                  </div>
                </div>
              </div>
{/each}

              

              
            </div>
          </div>
        </section>