<template>
  <div>{{a}} <slot/> {{b}} = {{result}}</div>
</template>

<script>
import loadWasm from '@/libs/calculator.rs'

export default {
  props: {
    a: Number,
    b: Number,
  },
  data() {
    return {
      result: null
    }
  },
  beforeCreate() {
      loadWasm().then(result => {
          const add = result.instance.exports['add'];
          this.result = add(this.a, this.b)
      })
    }
}
</script>
