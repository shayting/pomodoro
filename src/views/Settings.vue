<template lang="pug">
#settings
  b-container
    b-row
      b-col(cols="12")
        h1.text-center 設定
      b-col(cols="12")
        b-table(:items="items" :fields="fields" @row-clicked='select')
          template(#cell(src)="data")
            audio(controls :src="require('@/assets/' + data.value)")
          template(#cell(select)="data")
            span(v-if="data.item.src === sound") V
</template>
<!-- audio 標籤 產生播放器 -->
<!-- v-bind + require => 從assets裡面拉資料，沒有的話是從public裡拉資料 -->
<script>
export default {
  data () {
    return {
      items: [
        { name: '鬧鈴', src: 'alarm.mp3' },
        { name: 'yay', src: 'yay.mp3' }
      ],
      // 表頭 key 對應到 items的key
      fields: [
        { key: 'name', label: '名稱' },
        { key: 'src', label: '試聽' },
        { key: 'select', label: '選擇' }
      ]
    }
  },
  methods: {
    select (item) {
      console.log(item)
      this.$store.commit('selectSound', item.src)
    }
  },
  computed: {
    sound () {
      return this.$store.state.sound
    }
  }
}
</script>
