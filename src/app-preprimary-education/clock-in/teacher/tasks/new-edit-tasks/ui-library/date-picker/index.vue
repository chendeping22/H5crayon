<template>
  <imp-modal
    :show="visible"
    @close="closeModal"
    title="更新提示"
    confirm-text="立即更新"
    cancel-text="暂不更新"
  >
    <picker-view
      :indicator-style="indicatorStyle"
      :mask-style="maskStyle"
      :value="value"
      @change="bindChange"
    >
      <picker-view-column>
        <view class="item" v-for="(item, index) in years" :key="index">{{ item }}年</view>
      </picker-view-column>
      <picker-view-column>
        <view class="item" v-for="(item, index) in months" :key="index">{{ item }}月</view>
      </picker-view-column>
      <picker-view-column>
        <view class="item" v-for="(item, index) in days" :key="index">{{ item }}日</view>
      </picker-view-column>
    </picker-view>
  </imp-modal>
</template>

<script>
export default {
    data () {
        const date = new Date()
        const years = []
        const year = date.getFullYear()
        const months = []
        const month = date.getMonth() + 1
        const days = []
        const day = date.getDate()

        for (let i = 1990; i <= date.getFullYear(); i++) {
            years.push(i)
        }

        for (let i = 1; i <= 12; i++) {
            months.push(i)
        }

        for (let i = 1; i <= 31; i++) {
            days.push(i)
        }
        return {
            title: 'picker-view',
            years,
            year,
            months,
            month,
            days,
            day,
            value: [9999, month - 1, day - 1],
/**
 * 解决动态设置indicator-style不生效的问题
 */
            visible: true,
            // indicatorStyle: `height: ${Math.round(uni.getSystemInfoSync().screenWidth/(750/100))}px;`
            indicatorStyle: `height: 50px;`,
// #ifdef MP-KUAISHOU
maskStyle: "padding:10px 0"
// #endif
// #ifndef MP-KUAISHOU
maskStyle: ""
// #endif
        }
    },
    emits:['change'],
    methods: {
        bindChange (e) {
            const val = e.detail.value
            this.year = this.years[val[0]]
            this.month = this.months[val[1]]
            this.day = this.days[val[2]]
            this.$emits('change',val)
        }
    }
}
</script>

<style lang="scss">
picker-view {
  width: 100%;
  height: 600rpx;
  margin-top: $ui-gap-small;
}
.date-picker {
  width: 100%;
}
.item {
  line-height: 100rpx;
  text-align: center;
}
</style>
