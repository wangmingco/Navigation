<template>
  <div class="vc89-home">
    <div class="header">
      <h1>VC89 导航中心</h1>
      <p>欢迎使用 VC89 系列服务</p>
    </div>

    <div class="container">
      <el-row :gutter="30">
        <el-col
          v-for="(site, index) in sites"
          :key="index"
          :xs="24"
          :sm="12"
          :md="8"
          :lg="6"
        >
          <el-card class="site-card" shadow="hover" @click.native="goTo(site.url)">
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
    </div>

    <div class="footer">
      &copy; {{ new Date().getFullYear() }} VC89. All rights reserved.
    </div>
  </div>
</template>

<script>
export default {
  name: 'Vc89HomePage',
  data() {
    return {
      sites: [
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
      ]
    }
  },
  methods: {
    goTo(url) {
      // 在新标签页打开子站点（避免离开导航页）
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

.site-card {
  height: 280px;
  cursor: pointer;
  transition: all 0.3s ease;
  border-radius: 12px;
  overflow: hidden;
}

.site-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.12) !important;
}

.card-content {
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

.site-card h2 {
  font-size: 20px;
  color: #333;
  margin: 10px 0;
}

.site-card p {
  color: #666;
  font-size: 14px;
  margin-bottom: 16px;
  line-height: 1.5;
}

.goto-btn {
  background-color: #1e90ff;
  border-color: #1e90ff;
}

.footer {
  text-align: center;
  margin-top: 60px;
  color: #999;
  font-size: 14px;
}
</style>