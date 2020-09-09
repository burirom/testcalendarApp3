<template>
  <v-row class="fill-height">
    <v-col>
      <v-toolbar-title v-if="$refs.calendar">
        {{ $refs.calendar.title }}
      </v-toolbar-title>
      <div class="d-flex calendar">
        <div class="calendar-side">
          <div class="calendar-side-box">かれんだーサーチ</div>
          <div>
            <ReserveMonthBox
              :number-of-reservations-per-month="
                apiData.numberOfReservationsPerMonth
              "
            />
          </div>
        </div>
        <div class="calendar-box">
          <div class="calendar-header d-flex">
            <div
              v-for="(dayOfTheWeekList, index) in dayOfTheWeekLists"
              :key="index"
              class="calendar-header-content d-flex justify-center align-center"
            >
              {{ dayOfTheWeekList }}
            </div>
          </div>
          <div class="calendar-prop-box-content">
            <div class="calendar-box-content">
              <v-calendar
                ref="calendar"
                v-model="focus"
                :events="events"
                :event-color="getEventColor"
                :type="type"
                @click:more="viewDay"
                @click:date="viewDay"
                @change="updateRange"
              ></v-calendar>
            </div>
          </div>
        </div>
      </div>
      <!-- </v-sheet> -->
    </v-col>
  </v-row>
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
  data: () => ({
    focus: new Date('2020/7/31/10:10'),
    type: 'month',
    typeToLabel: {
      month: 'Month',
      week: 'Week',
      day: 'Day',
      '4day': '4 Days',
    },
    selectedEvent: {},
    selectedElement: null,
    selectedOpen: false,
    events: [],
    colors: [
      'blue',
      'indigo',
      'deep-purple',
      'cyan',
      'green',
      'orange',
      'grey darken-1',
    ],
    names: [
      'Meeting',
      'Holiday',
      'PTO',
      'Travel',
      'Event',
      'Birthday',
      'Conference',
      'Party',
    ],
    dayOfTheWeekLists: ['日', '月', '火', '水', '木', '金', '土'],
  }),
  mounted() {
    this.$refs.calendar.checkChange()
  },
  methods: {
    viewDay() {
      this.focus = new Date('2020/7/31/10:10')
      this.type = 'day'
    },
    getEventColor(event) {
      return event.color
    },
    prev() {
      this.$emit('setMonthText', this.$refs.calendar.title)
      this.$refs.calendar.prev()
    },
    next() {
      this.$emit('setMonthText', this.$refs.calendar.title)
      this.$refs.calendar.next()
    },
    updateRange() {
      const events = []
      for (let i = 0; i < this.customerLists.length; i++) {
        const first = new Date(this.customerLists[i].start)
        const second = new Date(this.customerLists[i].end)
        events.push({
          name: this.customerLists[i].name,
          start: first,
          end: second,
          color: '#000',
          timed: true,
        })
      }
      this.events = events
    },
  },
}
</script>
<style lang="scss" scoped>
.calendar {
  height: 600px;
  width: 100%;
}
.calendar-side {
  width: 200px;
  height: 100%;
  border-left: 1px solid #e0e0e0;
  .calendar-side-box {
    background: #f7f7f7;
    height: 60px;
    border-bottom: 1px solid #e0e0e0;
  }
}
.calendar-box {
  width: 100%;
  .calendar-header {
    background: #f7f7f7;
    height: 60px;
    .calendar-header-content {
      width: calc(100% / 7);
      border-left: 1px solid #e0e0e0;
    }
  }
  .calendar-box-content {
    height: 100%;
  }
  .calendar-prop-box-content {
    overflow-x: hidden;
    height: calc(100% - 60px);
  }
}
</style>
<style lang="scss">
.v-calendar-weekly__head {
  display: none !important;
}
</style>
