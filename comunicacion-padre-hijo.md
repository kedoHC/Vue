# Comunicacion entre un componente Padre a su componente Hijo en Vue

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
> 3. Insertamos el componente Hijo en el PADRE

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
> 4. Creamos las props que va a utilizar el componente HIJO, por ejemplo: que sea un arreglo y sea requerido.

```javascript

props: {
      listacompleta:{
            type: Array,
            required: true
      }
}

```
> 5. Guardamos en una propiedad del PADRE la info a pasar al HIJO, NO Olvidar el formato establecido de props en el Hijo, si es un Objeto o Array, etc y si es requerido. En este ejemplo consumimos un servicio que esta en lista.js que devuelve un Arreglo.

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
> 6. Colocamos las props en el HTML del HIJO insertado en el HTML del PADRE. Es muy importante el v-bind o : para "bindear" el valor.

```javascript

<Hijo :listacompleta="List" />

```