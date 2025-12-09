<template>
  <div class="vc89-home">
    <!-- 我的站点 -->
    <div class="header">
      <h1>VC89 导航中心</h1>
      <p>一站式访问我的服务与常用工具</p>
    </div>

    <div class="container">
      <!-- 我的站点（大卡片） -->
      <h2 class="section-title">我的站点</h2>
      <el-row :gutter="30" class="my-sites">
        <el-col
          v-for="(site, index) in mySites"
          :key="'my-' + index"
          :xs="24"
          :sm="12"
          :md="8"
          :lg="6"
        >
          <el-card class="site-card large" shadow="hover" @click.native="goTo(site.url)">
            <div class="card-content">
              <div class="icon-wrapper">
                <i :class="site.icon" class="site-icon"></i>
              </div>
              <h2>{{ site.title }}</h2>
              <p>{{ site.desc }}</p>
              <el-button type="primary" size="small" class="goto-btn">进入</el-button>
            </div>
          </el-card>
        </el-col>
      </el-row>

      <!-- 分类书签 -->
      <div v-for="(group, idx) in categorizedBookmarks" :key="idx" class="bookmark-group">
        <h2 class="section-title">{{ group.category }}</h2>
        <el-row :gutter="15">
          <el-col
            v-for="(item, i) in group.items"
            :key="`${idx}-${i}`"
            :xs="12"
            :sm="8"
            :md="6"
            :lg="4"
            :xl="3"
          >
            <el-card class="site-card small" shadow="hover" @click.native="goTo(item.url)">
              <div class="card-content">
                <h3 class="bookmark-title">{{ item.title }}</h3>
              </div>
            </el-card>
          </el-col>
        </el-row>
      </div>
    </div>

    <div class="footer">
      &copy; {{ new Date().getFullYear() }} VC89. All rights reserved.
    </div>
  </div>
</template>

<script>
import { categorizedBookmarks } from '@/assets/bookmarks.js'

export default {
  name: 'Vc89HomePage',
  data() {
    return {
      mySites: [
        { title: '愿望清单', desc: '管理你的愿望与心愿单', url: 'https://w.vc89.cn/', icon: 'el-icon-star-off' },
        { title: '金融站点', desc: '个人财务管理与记录', url: 'https://f.vc89.cn/', icon: 'el-icon-money' },
        { title: '进口原研药目录', desc: '权威原研药品信息查询', url: 'https://m.vc89.cn/', icon: 'el-icon-medical' },
        { title: '溜娃指南针', desc: '亲子出行、博物馆、乐园推荐', url: 'https://vc89.cn/', icon: 'el-icon-location-outline' }
      ],
      categorizedBookmarks
    }
  },
  methods: {
    goTo(url) {
      window.open(url, '_blank');
    }
  }
}
</script>

<style scoped>
/* ... 保留之前的所有样式 ... */

.bookmark-group {
  margin-bottom: 40px;
}

.section-title {
  margin: 40px 0 20px;
  font-size: 22px;
  color: #1d3f7f;
  text-align: left;
  padding-left: 10px;
  border-left: 4px solid #1e90ff;
}

/* 小卡片样式 */
.site-card.small {
  height: 100px;
  cursor: pointer;
  transition: all 0.2s;
}
.site-card.small:hover {
  transform: translateY(-3px);
  box-shadow: 0 4px 12px rgba(0,0,0,0.1) !important;
}
.bookmark-title {
  font-size: 14px;
  font-weight: 500;
  color: #333;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  text-align: center;
  line-height: 1.4;
  padding: 0 8px;
}
</style>