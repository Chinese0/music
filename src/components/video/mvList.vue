<template>
  <div v-if="videoList" class="maxBox">
    <div
      :class="(index + 1) % 3 ? 'itemBox' : 'itemBox cr'"
      v-for="(item, index) in videoList"
      :key="index"
    >
      <div class="imgBox" @click="putVideoing(videoList[index])">
        <img :src="item.cover" alt="" />
        <span class="time">{{ item.duration | timeFormat }}</span>
        <span class="count"
          ><i class="el-icon-view" style="color: #fff; margin-right: 4px"></i
          >{{
            item.playCount > 10000
              ? (item.playCount / 10000).toFixed(0) + "万"
              : item.playCount
          }}</span
        >
      </div>
      <div class="boFang"><i class="el-icon-video-play"></i></div>
      <div class="textBox">
        <h5 class="nowp">作者:{{ item.artistName }}</h5>
        <span class="nowp">{{ item.name }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import { timeFormat } from "common/tool";
export default {
  data() {
    return {};
  },
  props: {
    videoList: {
      type: Array,
    },
  },
  components: {},
  created() {
    console.log(this.videoList);
  },
  mounted() {
    console.log(this.videoList);
  },
  methods: {
    //跳转到视频播放
    putVideoing(info) {
      this.$store.commit("setVideoInfo", info);
      this.$router.push("/home/mving" + info.id);
      // console.log(info);
    },
  },
  watch: {
    idList: function () {
      this.getVideoList();
    },
  },
  filters: {
    timeFormat: function (value) {
      return timeFormat(value);
    },
  },
};
</script>

<style lang='less' scoped>
.maxBox {
  margin: 20px 0;
}
.itemBox {
  position: relative;
  float: left;
  margin-right: 15px;
  margin-bottom: 35px;
  h5 {
    display: inline-block;
    margin: 5px 0;
    font-size: 13px;
    font-weight: 400;
    width: 280px;
  }
  span {
    display: block;
    font-size: 13px;
    color: #444;
  }
}
.imgBox {
  position: relative;
  float: left;
  width: 300px;
  height: 170px;
  padding: 0 auto;
  background-color: #000;
  cursor: pointer;
  span {
    color: #fff;
  }
  img {
    max-height: 170px;
    max-width: 300px;
    margin-left: 50%;
    // transform: translate(-50%, -50%);
    transform: translateX(-50%);
  }
  .time {
    position: absolute;
    left: 7px;
    bottom: 3px;
  }
  .count {
    position: absolute;
    right: 7px;
    top: 5px;
  }
}
.boFang {
  position: absolute;
  bottom: 47px;
  right: 8px;
  font-size: 31px;
  i {
    color: rgba(255, 255, 255, 0.95);
  }

  transform: translateX(115%);
  transition: 0.3s;
}
.itemBox:hover .boFang {
  transform: translateY(0);
}
.textBox {
  span {
    width: 280px;
  }
}
</style>