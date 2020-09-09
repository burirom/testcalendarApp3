```
<template>
  <div>
    <ReserveCalendarCommon
      v-if="radios"
      :times="times"
      :first-lists="apiData.unitLists"
      :second-lists="apiData.terapisLists"
      :radios="radios"
      :customer-lists="customerLists"
      :date-item="dateItem"
      :business-time="apiData.business_time"
    >
    </ReserveCalendarCommon>
    <ReserveCalendarCommon
      v-else
      :times="times"
      :first-lists="apiData.terapisLists"
      :second-lists="apiData.unitLists"
      :radios="radios"
      :customer-lists="customerLists"
      :date-item="dateItem"
      :business-time="apiData.business_time"
    >
    </ReserveCalendarCommon>
  </div>
</template>
<script>
export default {
  props: {
    dateItem: {
      type: Object,
      default: null,
    },
    apiData: {
      type: Object,
      default: null,
    },
    customerLists: {
      type: Array,
      default: null,
    },
    radios: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      times: [],
    }
  },
  created() {
    if (this.apiData) this.setTimes()
  },
  methods: {
    setTimes() {
      this.times = []
      const businesstTime = this.calcBusinessTime(
        this.apiData.business_time.open,
        this.apiData.business_time.close
      )
      const startHour = this.apiData.business_time.open.getHours()
      for (let i = 0; i <= businesstTime; i++) {
        this.times.push(startHour + i + ':00')
      }
    },
    radiosEvent() {
      this.$emit('sendRaiosData', 'person')
    },
    // calc
    // calc Business Time diff
    calcBusinessTime(startDate, endDate) {
      const difftime = endDate.getHours() - startDate.getHours()
      return difftime
    },
    DateComparison(dateItem, date) {
      if (!dateItem) return false
      if (dateItem.year !== date.getFullYear()) return false
      if (dateItem.month !== date.getMonth() + 1) return false
      if (dateItem.day !== date.getDate()) return false
      return true
    },
    arryFindIdIndex(Id, Lists) {
      const resault = Lists.findIndex((object) => {
        return object.id === Id
      })
      return resault
    },
    calcReservationBigBoxPlaceX(Id, Lists) {
      const result = this.arryFindIdIndex(Id, Lists)
      if (result >= 0) return result
      return null
    },
    calcReservationBoxPlaceY(openDate, reservationDate) {
      const diffHours = Math.abs(
        openDate.getHours() - reservationDate.getHours()
      )
      const diffMinitu =
        ((diffHours * 60 + reservationDate.getMinutes()) / 10) * 20
      return diffMinitu
    },
    calcReservationSmallBoxPlaceX(unitId, unitLists, personId, personLists) {
      const unitIdIndex = this.arryFindIdIndex(unitId, unitLists)
      const personIdIndex = this.arryFindIdIndex(personId, personLists)
      const unitPlaceX = unitIdIndex * this.apiData.terapisLists.length
      const personPlaceX = personIdIndex
      return unitPlaceX + personPlaceX
    },
  },
}
</script>
