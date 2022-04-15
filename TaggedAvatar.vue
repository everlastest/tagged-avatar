<template>
  <div class="avatar" :style="{backgroundImage:'url('+imgUrl+')'}">
    <div ref="tag" class="tag" @mouseover="showFullName" @mouseleave="hideFullName">
      <span class="ranking">{{ placing }}</span>
      <span class="name">{{ name }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Avatar",
  props: ['placing', 'name', 'imgUrl'],
  data() {
    return {
      timer: null,
      sign: true,
    }
  },
  mounted() {
    this.changeWidth(this.$refs.tag)
  },
  methods: {
    showFullName(e) {
      let tag = e.currentTarget
      if (this.timer) clearTimeout(this.timer)
      if (this.sign === true) {
        this.timer = setTimeout(() => {
          tag.style.transition = '0.5s linear'
          this.sign = false
          this.changeWidth(tag)
        }, 100)
      }
    },
    hideFullName(e) {
      let tag = e.currentTarget
      if (this.timer) clearTimeout(this.timer)
      if (this.sign === false) {
        this.timer = setTimeout(() => {
          this.sign = true
          this.changeWidth(tag)
        }, 100)
      }
    },
    changeWidth(tag) {
      if (this.sign === false)
        tag.style.maxWidth = 'none'
      else {
        tag.style.maxWidth = '70px'
      }
      let width = tag.clientWidth
      tag.style.transform = 'translateX(-' + width / 2 + 'px)'
    }

  }
}
</script>

<style scoped>
.avatar {
  display: inline-block;
  position: relative;
  width: 70px;
  height: 70px;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  border-radius: 50%;
  border: 5px solid #B5D0D0;
}

.tag {
  position: absolute;
  left: 50%;
  bottom: -10px;
  height: 25px;
  line-height: 25px;
  min-width: 20px;
  max-width: 70px;
  padding: 0 5px;
  text-align: center;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
  color: #F5B767;
  border-radius: 8px;
  background-color: #ffffff;
  box-shadow: 0 0 15px #cdcdcd;
  opacity: 0.9;
}

.ranking {
  margin-right: 5px;
  font-weight: bold;
  color: #acacac;
}

.name {
  font-weight: bold;
  color: #F5B767;
}
</style>
