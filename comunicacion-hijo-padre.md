# Comunicación entre componentes Hijo-Padre en Vue JS

La comunicación entre un componente HIJO con su componente PADRE se da a través de eventos. El cual emite el HIJO y se configura el PADRE para que este pendiente



> 1. Creamos el componente PADRE

```javascript
<template>
      <div class="componente__padre">
            <p class="texto__selecccionado">
                  {{mensaje}}
            </p>
      </div>
      
</template>
<script>
export default {
      data (){
            return {
                  mensaje: "hello Vue's!!!"
            }
      }
}
</script>
```
> 2. Lo integramos con en el componente principal o en su respectivio componente PADRE.
>     1. Importando el componente.
>     2. Agregandolo en el objeto "components".
>     3. En el template.
```javascript
<template>
  <div id="app">
   <padre></padre>
  </div>
</template>

<script>
import Padre from './components/Padre.vue'

export default {
  name: 'app',
  data () {
    return {

    }
  },
  components:{
    Padre
  }
}
</script>
```
> Creamos el componente HIJO

Para este ejemplo creamos un arreglo en el return de la función data para mostrar los items de un menú.
```javascript
<template>
      <div class="componente__hijo">
            <ul>
                  <li v-for="item in items">
                        <p>{{item}}</p>
                  </li>
            </ul>
      </div>
      
</template>
<script>
export default {
      data (){
            return {
                  items: ["home", "visit", "blog", "contact"]
            }
      }
}
</script>

```
Vamos a detectar el click sobre casa uno de estos elementos y pasarle el nombre del item al componente PADRE. El cual mostrara en una etiqueta `<p>` ya en el template del PADRE.

> Creamos el evento en el componente HIJO. Agregando en al elemento `<p>` la directiva `@click` con el nombre del método que se ejecutará al detectar el evento y de parametro, ya que estamos iterando el arreglo items a traves de la directiva `v-for`, mandamos item, que contienen el nombre del item del menú.
```javascript
<template>
      <div class="componente__hijo">
            <ul>
                  <li v-for="item in items">
                        <p @click="clickItem(item)" >{{item}}</p>
                  </li>
            </ul>
      </div>
</template>
```

> Creamos el método en el objeto methods del comeponente

```javascript
<script>
export default {
      data (){
            return {
                  items: ["home", "visit", "blog", "contact"]
            }
      },
      methods: {
            clickItem(item) {
                  this.$emit('clickItemMenu', item)
            }
      }
}
```

> Se pueden observar que `clickItem(item)` recibe el parámetro que envia el evento y dentro de este método utilizamos la función de Vue, $emit, que nos permite "emitir" un evento que el padre pueda escuchar.
```javascript
this.$emit('clickItemMenu', item)
```
> Recibe 2 parametros: el nombre del evento que va a escuchar el PADRE y la información que se envía. 
> Con esto tenemos listo el componente HIJO emitiendo el evento que el padre necesita escuchar pero necesitamos decirle que escuchar.

> En el componente PADRE, en el elemento html del componente HIJO colocamos el evento que va a escuchar el padre. El nombre que se colocó dentro de la función $emit en el HIJO y colocamos el nombre del método dentro de PADRE que se ejecutará.
```html
<hijo @clickItemMenu="mostrarNombreItem"></hijo>
```
> Creamos el método del padre
```javascript
<script>
import Hijo from './Hijo.vue'

export default {
      data (){
            return {
                  mensaje: "hello bitches!!!",
                  itemClick: ''
            }
      },
      components: {
            Hijo
      },
      methods: {
            mostrarNombreItem(item){
                  this.itemClick = item
            }
      }
}
</script>
```

> También cremos una variable `itemClick: ''` dentro del return del PADRE para almacenar el valor del item que pasa el componente HIJO, esto dentro del metodo que `mostrarNombreItem`.
> Ya con el valor del item del menú guardado en `itemClick` podemos utilizarlo en el template del PADRE.

```html
<p>Item del Menú clickeado: {{this.itemClick}}</p>
```














