<template>
  <div class="wrapper card">
    <!-- 资源图片 -->
    <div class="poster-wrapper">
      <img
        :src="image"
        class="poster">
    </div>
    <!-- 资源信息 -->
    <div class="info-box">
      <div class="resource-title fs-20">
        {{ title }}
      </div>
      <!-- 资源标记 -->
      <div class="resource-mark-info">
        <gd-button @click.native="resourceMarkDialogVisible = true">想看</gd-button>
        <gd-button @click.native="resourceMarkDialogVisible = true">在看</gd-button>
        <gd-button @click.native="resourceMarkDialogVisible = true">看过</gd-button>
      </div>
    </div>
    <!-- 评分信息 -->
    <div class="score-box">
      <div class="score-title">豆瓣评分</div>
      <div
        v-if="ratingValue"
        class="rating-value">
        {{ Number(ratingValue).toFixed(1) }}
        <span class="rating-value-slash">/</span>
        <span class="rating-value-total">10</span>
      </div>
      <div v-else>
        尚无评分
      </div>
      <div v-if="ratingCount">
        {{ ratingCount }} 人评价
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex';
import Button from '../components/button';

export default {
  components: {
    'gd-button': Button
  },
  data() {
    return {
      resourceMarkDialogVisible: false
    };
  },
  props: ['image', 'title', 'id', 'ratingValue', 'ratingCount'], //eslint-disable-line
  methods: {
    ...mapActions(['markResource'])
  }
};
</script>

<style scoped>
.wrapper {
  position: relative;
  width: 700px;
  margin: 40px auto;
  padding: 20px;
  min-height: 150px;
  display: flex;
}

.poster-wrapper {
  width: 120px;
  height: 160px;
  position: absolute;
  top: -24px;
  left: 20px;
  box-shadow: 0 4px 20px 0 rgba(0, 0, 0, 0.3);
  border-radius: 1px;
}

.poster {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 100%;
  transform: translate(-50%, -50%);
  object-fit: cover;
  height: 100%;
}

.info-box {
  flex: 1;
  margin-left: 137px;
}
.resource-title {
  padding-right: 20px;
  font-weight: bolder;
  color: white;
}

.score-box {
  border-left: 1px solid hsla(0, 0%, 100%, 0.1);
  width: 144px;
  text-align: left;
  padding-left: 30px;
}

.score-title {
  color: rgba(255, 255, 255, 0.3);
}

.rating-value {
  color: #fff280;
  font-size: 42px;
}

.rating-value-slash {
  font-size: 12px;
  color: rgba(255, 255, 255, 0.3);
}

.rating-value-total {
  font-size: 12px;
  color: rgba(255, 255, 255, 0.3);
}

.resource-mark-info {
  position: absolute;
  bottom: 15px;
}
</style>
