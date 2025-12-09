<template>
  <div class="vc89-home">
    <!-- 顶部标题 -->
    <div class="header">
      <h1>VC89 导航中心</h1>
      <p>一站式访问我的服务与常用工具</p>
    </div>

    <div class="container">
      <!-- 我的站点（大卡片，完全不变） -->
      <h2 class="section-title">我的站点</h2>
      <el-row :gutter="30">
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
              <el-button type="primary" size="small" class="goto-btn">进入站点</el-button>
            </div>
          </el-card>
        </el-col>
      </el-row>

      <!-- 分类书签（超小卡片） -->
      <div v-for="(group, idx) in categorizedBookmarks" :key="idx" class="bookmark-group">
        <h2 class="section-title">{{ group.category }}</h2>
        <div class="bookmarks-row">
          <span
            v-for="(item, i) in group.items"
            :key="`${idx}-${i}`"
            class="bookmark-tag"
            @click="goTo(item.url)"
          >
            {{ item.title }}
          </span>
        </div>
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
        {
          title: '愿望清单',
          desc: '管理你的愿望与心愿单',
          url: 'https://w.vc89.cn/',
          icon: 'el-icon-star-off'
        },
        {
          title: '金融站点',
          desc: '个人财务管理与记录',
          url: 'https://f.vc89.cn/',
          icon: 'el-icon-money'
        },
        {
          title: '进口原研药目录',
          desc: '权威原研药品信息查询',
          url: 'https://m.vc89.cn/',
          icon: 'el-icon-medical'
        },
        {
          title: '溜娃指南针',
          desc: '亲子出行、博物馆、乐园推荐',
          url: 'https://vc89.cn/',
          icon: 'el-icon-location-outline'
        }
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
.vc89-home {
  min-height: 100vh;
  background: linear-gradient(135deg, #f5f7fa 0%, #e4edf9 100%);
  padding: 20px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.header {
  text-align: center;
  margin: 40px 0 50px;
}

.header h1 {
  font-size: 36px;
  color: #1d3f7f;
  margin-bottom: 12px;
}

.header p {
  color: #666;
  font-size: 18px;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

/* —————— 我的站点：大卡片（完全保留原样式） —————— */
.site-card.large {
  height: 280px;
  cursor: pointer;
  border-radius: 12px;
  transition: all 0.3s ease;
  overflow: hidden;
}

.site-card.large:hover {
  transform: translateY(-6px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.12) !important;
}

.site-card.large .card-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  text-align: center;
  padding: 20px;
}

.icon-wrapper {
  width: 72px;
  height: 72px;
  background: rgba(30, 144, 255, 0.1);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 16px;
}

.site-icon {
  font-size: 32px;
  color: #1e90ff;
}

.site-card.large h2 {
  font-size: 20px;
  color: #333;
  margin: 10px 0;
}

.site-card.large p {
  color: #666;
  font-size: 14px;
  margin-bottom: 16px;
  line-height: 1.5;
}

.goto-btn {
  background-color: #1e90ff;
  border-color: #1e90ff;
}

/* —————— 三方站点：超小标签（宽高 ≈ 原小卡片的 1/3） —————— */
.bookmark-group {
  margin: 50px 0 40px;
}

.bookmarks-row {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  padding: 0 10px;
}

.bookmark-tag {
  display: inline-block;
  height: 36px;
  line-height: 34px;
  padding: 0 14px;
  background: #fff;
  color: #1d3f7f;
  border: 1px solid #dbe2ee;
  border-radius: 6px;
  font-size: 13px;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: calc((100% - 40px) / 3); /* 约 1/3 宽度（考虑 gap） */
}

.bookmark-tag:hover {
  background: #1e90ff;
  color: white;
  border-color: #1e90ff;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(30, 144, 255, 0.2);
}

/* —————— 分类标题 —————— */
.section-title {
  margin: 50px 0 25px;
  font-size: 24px;
  color: #1d3f7f;
  text-align: center;
  position: relative;
}

.section-title::after {
  content: '';
  display: block;
  width: 40px;
  height: 3px;
  background: #1e90ff;
  margin: 8px auto 0;
  border-radius: 2px;
}

/* —————— 页脚 —————— */
.footer {
  text-align: center;
  margin-top: 60px;
  color: #999;
  font-size: 14px;
}

/* 响应式：手机端每行 2 个 */
@media (max-width: 768px) {
  .bookmark-tag {
    max-width: calc((100% - 10px) / 2);
  }
}
</style>