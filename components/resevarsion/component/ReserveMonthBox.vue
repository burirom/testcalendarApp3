<template>
  <div>
    <div>月間予約件数</div>
    <div>
      <div
        v-for="(terapisList,
        index) in numberOfReservationsPerMonth.terapisLists"
        :key="index"
        class="numberItem d-flex"
      >
        <div>
          {{ terapisList.terapisName }}
        </div>
        <div class="ml-auto">
          <span class="pl-3 pr-1">{{ terapisList.Number }}</span
          >件
        </div>
      </div>
      <div class="d-flex numberItem">
        <div>合計</div>
        <div class="ml-auto">
          <span class="pl-3 pr-1">{{
            numberOfReservationsPerMonth.TotalNumber
          }}</span
          >件
        </div>
      </div>
    </div>
    <div>
      <div class="d-flex numberItem">
        <div>空き枠</div>
        <div class="ml-auto">
          <span class="pl-3 pr-1">{{
            numberOfReservationsPerMonth.EmptyFrame
          }}</span
          >枠
        </div>
      </div>
      <div class="d-flex">
        <div v-for="num of 10" :key="num.id" class="no-active-box"></div>
      </div>

      <div class="d-flex numberItem">
        <div>稼働率</div>
        <div class="ml-auto">
          <span class="pl-3 pr-1">{{
            numberOfReservationsPerMonth.EmptyFrame
          }}</span
          >%
        </div>
      </div>
      <div class="d-flex">
        <div v-for="num of 10" :key="num.id" class="no-active-box"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    numberOfReservationsPerMonth: {
      type: Object,
      default: null,
    },
  },
}
</script>

<style lang="scss" scoped>
.numberItem {
  span {
    color: #004adb;
    font-size: 22px;
  }
}

.no-active-box {
  height: 14px;
  width: 10px;
  background: #004adb;
}
</style>
