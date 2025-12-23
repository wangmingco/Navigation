<template>
  <div class="vc89-home">
    <!-- 右上角联系按钮 -->
    <div class="contact-btn" @click="contactMe">
      <i class="el-icon-message"></i> 联系我
    </div>

    <!-- 顶部标题 -->
    <div class="header">
      <h1>VC89 导航中心</h1>
      <p>一站式访问我的服务与常用工具</p>
    </div>

    <div class="container">
      <!-- 我的站点（大卡片，强制一行显示，可横向滚动） -->
      <h2 class="section-title">我的站点</h2>
      <div class="my-sites-container">
        <div class="my-sites-row">
          <el-card
            v-for="(site, index) in mySites"
            :key="'my-' + index"
            class="site-card large"
            shadow="hover"
            @click.native="goTo(site.url)"
          >
            <div class="card-content">
              <div class="icon-wrapper">
                <i :class="site.icon" class="site-icon"></i>
              </div>
              <h2>{{ site.title }}</h2>
              <p>{{ site.desc }}</p>
              <el-button type="primary" size="small" class="goto-btn">进入站点</el-button>
            </div>
          </el-card>
        </div>
      </div>

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
          title: '溜娃指南针',
          desc: '亲子乐园、博物馆推荐',
          url: 'https://vc89.cn/',
          icon: 'el-icon-location-outline'
        },
        {
          title: '技术博客',
          desc: '我的技术博客',
          url: 'https://blog.vc89.cn/',
          icon: 'el-icon-document-copy'
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
          icon: 'el-icon-coffee'
        },
        {
          title: '愿望清单',
          desc: '管理你的愿望与心愿单',
          url: 'https://w.vc89.cn/',
          icon: 'el-icon-star-off'
        }
      ],
      categorizedBookmarks
    }
  },
  methods: {
    goTo(url) {
      window.open(url, '_blank');
    },
    contactMe() {
      window.location.href = 'mailto:admin@vc89.cn';
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
  position: relative;
}

/* —————— 右上角联系按钮 —————— */
.contact-btn {
  position: absolute;
  top: 20px;
  right: 20px;
  background-color: #1e90ff;
  color: white;
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 14px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 4px;
  box-shadow: 0 2px 6px rgba(30, 144, 255, 0.4);
  z-index: 10;
  transition: background-color 0.2s;
}

.contact-btn:hover {
  background-color: #0d7ae0;
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

/* —————— 我的站点：强制一行显示，横向滚动，卡片等宽 —————— */
.my-sites-container {
  overflow-x: auto;
  padding: 10px 0 10px;
  margin-bottom: 30px;
  -webkit-overflow-scrolling: touch;
  /* 隐藏滚动条 */
  scrollbar-width: none; /* Firefox */
}

.my-sites-container::-webkit-scrollbar {
  display: none; /* Chrome, Safari */
}

.my-sites-row {
  display: flex;
  gap: 20px;
  padding: 0 15px;
  min-width: max-content;
}

.my-sites-row .site-card.large {
  flex: 0 0 220px; /* 固定宽度，保证所有卡片等宽 */
  height: 280px;
  cursor: pointer;
  border-radius: 12px;
  transition: all 0.3s ease;
  overflow: hidden;
}

.my-sites-row .site-card.large:hover {
  transform: translateY(-6px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.12) !important;
}

.my-sites-row .site-card.large .card-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100%;
  text-align: center;
  padding: 20px;
}

/* —————— 大卡片内部样式 —————— */
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

.my-sites-row .site-card.large h2 {
  font-size: 20px;
  color: #333;
  margin: 10px 0;
}

.my-sites-row .site-card.large p {
  color: #666;
  font-size: 14px;
  margin-bottom: 16px;
  line-height: 1.5;
}

.goto-btn {
  background-color: #1e90ff;
  border-color: #1e90ff;
}

/* —————— 三方站点：超小标签 —————— */
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
  max-width: calc((100% - 40px) / 3);
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

  .contact-btn {
    top: 10px;
    right: 10px;
    padding: 4px 10px;
    font-size: 13px;
  }
}
</style>