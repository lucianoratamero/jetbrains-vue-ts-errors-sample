<template>
  <section>
    With any nested object, it errors with "Unresolved variable"
    {{ data?.obj1 }}
    {{ data?.obj1.obj2 }}
    <template v-if="data">
      {{ data.obj1.obj2 }} "data"
    </template>
    <template v-if="refData">
      {{ refData.obj1.obj2 }} "refData"
    </template>
    <template v-if="toRefsData">
      {{ toRefsData?.obj1.obj2 }} "toRefsData"
    </template>
    <template v-if="obj1">
      {{ obj1.obj2 }} "obj1"
    </template>
  </section>

  <section>
    Here, somehow, obj2 becomes any
    <template v-if="obj2">
      {{ obj2 }} "obj2"
    </template>
  </section>

  <section>
    When ref object is nested, it errors
    <template v-if="refObj1">
      {{ refObj1.obj2 }} "refObj1.obj2"
    </template>
  </section>

  <section>
    When using directly, it recognizes as string
    <template v-if="refObj2">
      {{ refObj2 }} "refObj2"
    </template>
  </section>
</template>

<script setup lang="ts">
// all inference here in the script setup seems correct
// but in the template, everything is borked
import { ref, toRefs } from 'vue'

type Props = {
  data?: {
    obj1: {
      obj2: string
    }
  }
}

const props = defineProps<Props>()

// it doesn't matter if I inline the prop type
// const props = defineProps<{
//   data?: {
//     obj1: {
//       obj2: string
//     }
//   }
// }>()
const { data } = toRefs(props)

const { data: toRefsData } = toRefs({ data })

const obj1 = data?.value?.obj1 || { obj2: 'obj2' }
const { obj2 } = obj1
const refObj1 = ref(obj1)
const refObj2 = ref(obj2)
const refData = ref(data)
</script>