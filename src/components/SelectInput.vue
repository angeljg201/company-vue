<script setup>
import { onMounted, ref } from 'vue';

const props = defineProps({
  options: Array,
  modelValue: [String, Number], // Acepta tanto String como Number
})

defineEmits(['update:modelValue'])

const input = ref(null)

onMounted(() => {
    if(input.value.hasAttribute('autofocus')) {
        input.value.focus
    }
})

defineExpose({focus: () => input.value.focus() })

</script>

<template>
    <select 
        class="form-select"
        :value="modelValue"
        @change="$emit('update:modelValue', $event.target.value)"
        ref="input">
        <option v-for="op in options" :key="op.i" :value="op.id">
            {{ op.name }}
        </option>
    </select>
</template>


<!-- <script setup>
import { defineProps, defineEmits } from 'vue';

// Definir las propiedades que recibe el componente
const props = defineProps({
  options: Array,
  modelValue: [String, Number], // Acepta tanto String como Number
});

// Emitir el evento de actualización del valor
const emit = defineEmits(['update:modelValue']);
</script>

<template>
  <select
    class="form-select"
    :value="modelValue" 
    @change="$emit('update:modelValue', $event.target.value)" 
  >
    <option v-for="op in props.options" :key="op.id" :value="op.id">
      {{ op.name }}
    </option>
  </select>
</template> -->


