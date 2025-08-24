<template>
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <q-input
        filled
        v-model="ชื่อ นะครับ"
        label="ชื่อ ของคุณ นะครับ*"
        hint="ชื่อ-สกุล นะครับ"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาใส่ข้อมูลให้ถูกต้อง นะครับ']"
      />

      <q-input
        filled
        type="number"
        v-model="อายุ นะครับ"
        label="อายุของคุณ นะครับ*"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'กรุณาใส่อายุของคุณ นะครับ',
          val => val > 0 && val < 100 || 'กรุณาใส่อายุจริงของคุณ นะครับ'
        ]"
      />

      <q-toggle v-model="accept" label="I accept the license and terms" />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

export default {
  setup () {
    const $q = useQuasar()

    const name = ref(null)
    const age = ref(null)
    const accept = ref(false)

    return {
      name,
      age,
      accept,

      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'You need to accept the license and terms first'
          })
        }
        else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'Submitted'
          })
        }
      },

      onReset () {
        name.value = null
        age.value = null
        accept.value = false
      }
    }
  }
}
</script>
