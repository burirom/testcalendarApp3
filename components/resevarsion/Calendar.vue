<template>
  <div>
    <ReserveCalendarHeader
      :radios="raiosData"
      :month-text="monthText"
      @sendDate="setDate"
      @sendRaiosData="setRaiosData"
      @sendCarendarList="setCarendarActiveList"
      @prev="prev"
      @next="next"
    />
    <ReserveCalendarDayContent
      v-if="activeCarendarList === 'day'"
      :date-item="dateItem"
      :radios="raiosData === 'unit' ? true : false"
      :api-data="damyData"
      :customer-lists="damyData.customerLists"
      :width="100"
      @sendRaiosData="setRaiosData"
    />
    <!-- <ReserveCalendarWeekContent
      v-if="activeCarendarList === 'week'"
      :date-item="dateItem"
      :radios="raiosData === 'unit' ? true : false"
      :api-data="damyData"
      :customer-lists="damyData.customerLists"
      :width="100"
      @sendRaiosData="setRaiosData"
    />
    <ReserveCalendarHalfMonth
      v-if="activeCarendarList === 'custom-weekly'"
      :date-item="dateItem"
      :radios="raiosData === 'unit' ? true : false"
      :api-data="damyData"
      :customer-lists="damyData.customerLists"
      :width="100"
      @sendRaiosData="setRaiosData"
    /> -->
    <ReserveCalendarMonthContent
      v-if="activeCarendarList === 'month'"
      ref="CalendarMonthContent"
      :date-item="dateItem"
      :radios="raiosData === 'unit' ? true : false"
      :api-data="damyData"
      :customer-lists="damyData.customerLists"
      :width="100"
      @sendRaiosData="setRaiosData"
      @setMonthText="setMonthText"
    />
  </div>
</template>
<script>
export default {
  data() {
    return {
      date: new Date(),
      dateItem: {
        year: null,
        month: null,
        day: null,
      },
      raiosData: 'unit',
      activeCarendarList: 'day',
      monthText: '',
      damyData: {
        business_time: {
          open: new Date('2020/9/2/7:50'),
          close: new Date('2020/9/2/17:0'),
        },
        times: [],
        terapisLists: [
          {
            id: 1,
            terapisName: 'あ担当者1',
          },
          {
            id: 2,
            terapisName: 'い担当者2',
          },
          {
            id: 3,
            terapisName: 'う担当者３',
          },
          {
            id: 4,
            terapisName: 'え担当者４',
          },
          {
            id: 5,
            terapisName: 'お担当者5',
          },
          {
            id: 6,
            terapisName: 'お担当者5',
          },
          {
            id: 7,
            terapisName: 'お担当者5',
          },
        ],
        unitLists: [
          {
            id: 1,
            unitName: 'ユニット1',
          },
          {
            id: 2,
            unitName: 'ユニット2',
          },
          {
            id: 3,
            unitName: 'ユニット３',
          },
          {
            id: 4,
            unitName: 'ユニット４',
          },
          {
            id: 5,
            unitName: 'ユニット5',
          },
          {
            id: 6,
            unitName: 'ユニット４',
          },
          {
            id: 7,
            unitName: 'ユニット5',
          },
        ],
        customerLists: [
          {
            start: new Date('2020/8/31/10:10'),
            end: new Date('2020/8/31/13:0'),
            name: '野村',
            customerNumberOfPeople: 0,
            nomination: false,
            terapisNameId: 6,
            unitId: 2,
          },
          {
            start: new Date('2020/9/2/10:0'),
            end: new Date('2020/9/2/14:0'),
            name: '野村',
            customerNumberOfPeople: 0,
            nomination: true,
            terapisNameId: 6,
            unitId: 2,
          },
        ],
        numberOfReservationsPerMonth: {
          terapisLists: [
            {
              id: 1,
              terapisName: '植田',
              Number: 10,
            },
            {
              id: 2,
              terapisName: '吉田',
              Number: 20,
            },
            {
              id: 3,
              terapisName: '田中',
              Number: 30,
            },
            {
              id: 4,
              terapisName: '山田',
              Number: 40,
            },
            {
              id: 4,
              terapisName: '佐藤',
              Number: 40,
            },
            {
              id: 5,
              terapisName: '井上',
              Number: 100,
            },
            {
              id: 6,
              terapisName: '中村',
              Number: 8,
            },
          ],
          TotalNumber: 208,
          EmptyFrame: 20,
          OccupancyRate: 38,
        },
      },
    }
  },
  methods: {
    setDate(data) {
      this.dateItem.year = data.getFullYear()
      this.dateItem.month = data.getMonth() + 1
      this.dateItem.day = data.getDate()
    },
    setRaiosData(data) {
      this.raiosData = data
    },
    setCarendarActiveList(data) {
      this.activeCarendarList = data
    },
    prev() {
      this.$refs.CalendarMonthContent.prev('prev')
    },
    next() {
      this.$refs.CalendarMonthContent.next('next')
    },
    setMonthText(data) {
      this.monthText = data
    },
  },
}
</script>
