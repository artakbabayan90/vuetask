<template>
  <div class="column:grid-7 center:grid-items">
    <div v-for="cal in calendar" :key="cal" :class="['y:margin-1','width-100','center:text', {'gray-7:text':blurDate(cal),
    'none:event':disabledClickDate(cal), 'pointer:cursor':disabledClickDate(cal) === false}]"
         @click="eventDate(cal)">
      <div :class="['padding-2', {'green':resultDate === cal}]">{{ filterDate(cal) }}</div>
    </div>

  </div>
  <div :class="['center:flex','y:margin-2','green:text',{'d:none':resultDate === ''}]">
    {{resultDate}}
  </div>
</template>

<script>
import {ref} from 'vue'
import {$date as useDate} from 'alga-js'

export default ({
  name: "Calendar",
  setup() {
    const year = ref(0)
    const month = ref(0)
    const resultDate = ref('')

    const dateNow = new Date()
    year.value = dateNow.getFullYear()
    month.value = Number(dateNow.getMonth()) + 1

    const calendar = useDate.calendar(year.value, month.value)
    const getDayNames = calendar.slice(0, 7)

    const filterDate = (date) => {
      let newDate = ''
      if (getDayNames.includes(date)) {
        newDate = date.slice(0, 3)
      } else {
        const splitDate = date.split('-')
        newDate = splitDate[2]
      }
      return newDate
    }

    const blurDate = (date) => {
      let blurText = false
      if (!getDayNames.includes(date) && Number(date.split('-')[1]) !== month.value) {
        blurText = true
      }
      return blurText
    }

    const disabledClickDate = (date) => {
      let disabledClick = false
      if (getDayNames.includes(date) || Number(date.split('-')[1]) !== month.value) {
        disabledClick = true
      }
      return disabledClick
    }

    const eventDate = (date) => {
      resultDate.value = date
    }
    return {
      calendar,
      filterDate,
      blurDate,
      disabledClickDate,
      eventDate,
      resultDate
    }
  }
})
</script>

<style scoped>

</style>