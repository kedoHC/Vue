# Comunicacion entre un componente Padre a su componente Hijo en Vue

1. Creamos el componente PADRE

```javascript
<template>
      <div id="padre">
            <Hijo :listacompleta="List" />
      </div>
</template>
<script>
import Hijo from './Hijo.vue'
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
</script>
<style lang="scss">
      #padre{
            background: #eee;
      }
      #lista__nombres{
            padding-left: 0;
            margin: 0;
            list-style: none;
      }
</style>

```
2. Lo insertamos en el App.vue (en caso de ser parte)
2. Creamos el componente HIJO
3. Insertamos el componente Hijo en el PADRE
4. Creamos las props que va a utilizar el componente HIJO
5. Guardamos en una propiedad del PADRE la info a pasar al HIJO, NO Olvidar el formato establecido de props en el Hijo, si es un Objeto o Array, etc y si es requerido.
6. Colocamos las props en el HTML del HIJO insertado en el HTML del PADRE
7. NO OLVIDAR bindear el nombre de la propiedad