<template>
  <div>
    <!--search bar layout-->
    <div class="search-bar">
      <van-row>
        <van-col span="3">
          <img :src="locationIcon" width="80%" />
        </van-col>
        <van-col span="16">
          <input type="text" class="search-input" />
        </van-col>
        <van-col span="5">
          <van-button size="mini" class="search-btn">查找</van-button>
        </van-col>
      </van-row>
    </div>
    <!--swipwer area-->
    <div class="swiper-area">
      <van-swipe :autoplay="3000">
        <van-swipe-item v-for="(banner,index) in bannerPicArray" :key="index">
          <img v-lazy="banner.imageUrl" :src="banner.imageUrl" width="100%" />
        </van-swipe-item>
      </van-swipe>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      locationIcon: require("@/assets/images/location.png"),
      bannerPicArray: [
        {
          imageUrl: "https://api.zbztb.cn/pyg/banner1.png"
        },
        {
          imageUrl: "https://api.zbztb.cn/pyg/banner2.png"
        },
        {
          imageUrl: "https://api.zbztb.cn/pyg/banner3.png"
        }
      ]
    };
  },
  created() {
    axios({
      url: "https://api.zbztb.cn/api/public/v1/home/catitems",
      method: "get"
    })
      .then(response => {
        console.log(response);
      })
      .catch(error => {});
  }
};
</script>

<style scoped>
.search-bar {
  height: 2.2rem;
  background-color: #e5017d;
  overflow: hidden;
  line-height: 2.2rem;
}
.search-input {
  width: 100%;
  height: 1.3rem;
  border-top: 0px;
  border-left: 0px;
  border-right: 0px;
  border-bottom: 1px solid 1px !important ;
  background-color: #e5017d;
  color: #fff;
}
.search-btn {
  left: 20%;
  min-width: 2.5rem;
  height: 1.1rem;
  font-size: 0.5rem;
  line-height: 1.1rem;
}
.location-icon {
  padding-top: 0.2rem;
  padding-left: 0.3rem;
}
.swiper-area {
  width: 20rem;
  clear: both;
}
</style>