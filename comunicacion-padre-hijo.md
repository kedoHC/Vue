# Comunicacion entre componentes Padre-Hijo en Vue JS

La comunicación de un componente PADRE a un componente HIJO se realiza a través de PROPS, que son "propiedades" que puede o no esperar el componente hijo para realizar una acción. Es importante saber que la información que recibe el HIJO a través del PADRE es inmutable para el HIJO ya que no debe (como buena práctica) eliminar o modificar el contenido. Por lo cual solo debe utilizar funciones puras o como hace referencia en la documentación de VUE, que sean de SOLO LECTURA.

> 1. Creamos el componente PADRE

```javascript
<template>
      <div class="componente-padre">
      </div>
</template>
<script>
export default {
      data () {
            return {
                  
            }
      },
      components: {

      }
}
</script>
```
> 2. Lo insertamos en el App.vue (en caso de ser parte) o en un su propio componente PADRE

```javascript
<template>
  <div id="app">
    <Padre />    
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

> 2. Creamos el componente HIJO

```javascript
<template>
      <div class="componente-hijo">
            <ul>
                  <li>Item 1<li>
                  <li>Item 2<li>
                  <li>Item 3<li>
                  <li>Item 4<li>
            </ul>
      </div>
</template>
<script>
export default {
      data () {
            return {
                  
            }
      }
}
</script>
```
> 3. Insertamos el componente HIJO en el PADRE

```javascript
<template>
      <div class="componente-padre">
            <Hijo />
      </div>
</template>
<script>

import Hijo from './Hijo.vue'

export default {
      data () {
            return {
                  
            }
      },
      components: {
            Hijo
      }
}
</script>

```
> 4. Creamos las PROPS que va a utilizar el componente HIJO, con su nombre y sus propiedades, por ejemplo: que sea un arreglo y sea requerido.

```javascript

props: {
      listacompleta:{
            type: Array,
            required: true
      }
}

```
> 5. Guardamos en una propiedad del PADRE la información a pasar al HIJO, NO Olvidar el formato establecido de PROPS en el Hijo, si es un Objeto o Array, etc y si es requerido. En este ejemplo consumimos un servicio que está en lista.js que devuelve un Arreglo.

```javascript

import listacompleta from '../data/lista.js'

export default {
      data () {
            return {
                  List : listacompleta.items
            }
      },
      components: {
            Hijo
      }
}

```
> 6. Colocamos las PROPS en el HTML del HIJO insertado en el HTML del PADRE. Es muy importante el `v-bind` o `:` para "bindear" el valor.

```javascript

<Hijo :listacompleta="List" />

```

> 7 En el componente HIJO podemos iterar sobre el array "listacompleta" que es el "PROPS" que se esta pasando.

```javascript

<template>
      <ul id="lista__nombres">
            <li v-for="item in listacompleta">
                  {{item.nombre}} {{item.apellido}}
            </li>
      </ul>
</template>

<script>
export default {
      data () {
            return {

            }
      },
      props: {
            listacompleta:{
                  type: Array,
                  required: true
            }
      }

}
</script>

```

> Nos mostrara dentro del componente PADRE los datos del Arreglo.