<template>
  <div class="login-warp flex-center">
    <div class="login-background">
      <div class="gradient-layer"></div>
      <div class="decorative-shape shape-1"></div>
      <div class="decorative-shape shape-2"></div>
      <div class="decorative-shape shape-3"></div>
      <div class="decorative-shape shape-4"></div>
    </div>
    <div class="login-container w-full h-full">
      <el-row class="container w-full h-full">
        <el-col :xs="0" :sm="0" :md="12" :lg="12" :xl="14" class="left-container">
          <div class="login-hero">
            <div class="hero-content">
              <h1 class="hero-title">蓝星晴RAG</h1>
              <p class="hero-subtitle">智能问答 · 知识管理 · 高效协作</p>
              <div class="hero-features">
                <div class="feature-item">
                  <span class="feature-icon">🚀</span>
                  <span class="feature-text">快速部署</span>
                </div>
                <div class="feature-item">
                  <span class="feature-icon">💡</span>
                  <span class="feature-text">智能检索</span>
                </div>
                <div class="feature-item">
                  <span class="feature-icon">🤝</span>
                  <span class="feature-text">团队协作</span>
                </div>
              </div>
            </div>
          </div>
        </el-col>
        <el-col :xs="24" :sm="24" :md="12" :lg="12" :xl="10" class="right-container flex-center">
          <el-dropdown trigger="click" type="primary" class="lang" v-if="lang">
            <template #dropdown>
              <el-dropdown-menu class="w-180">
                <el-dropdown-item
                  v-for="(lang, index) in langList"
                  :key="index"
                  :value="lang.value"
                  @click="changeLang(lang.value)"
                  class="flex-between"
                >
                  <span :class="lang.value === user.getLanguage() ? 'primary' : ''">{{
                    lang.label
                  }}</span>

                  <el-icon
                    :class="lang.value === user.getLanguage() ? 'primary' : ''"
                    v-if="lang.value === user.getLanguage()"
                  >
                    <Check />
                  </el-icon>
                </el-dropdown-item>
              </el-dropdown-menu>
            </template>
            <el-button>
              {{ currentLanguage }}<el-icon class="el-icon--right"><arrow-down /></el-icon>
            </el-button>
          </el-dropdown>
          <slot></slot>
        </el-col>
      </el-row>
    </div>
  </div>
</template>
<script setup lang="ts">
import { computed } from 'vue'
import { getThemeImg } from '@/utils/theme'
import useStore from '@/stores'
import { useLocalStorage } from '@vueuse/core'
import { langList, localeConfigKey, getBrowserLang } from '@/locales/index'
defineProps({
  lang: {
    type: Boolean,
    default: true,
  },
})
const { user, theme } = useStore()

const changeLang = (lang: string) => {
  useLocalStorage(localeConfigKey, getBrowserLang()).value = lang
  window.location.reload()
}

const currentLanguage = computed(() => {
  return langList.value?.filter((v: any) => v.value === user.getLanguage())?.[0]?.label
})

const fileURL = computed(() => {
  if (theme.themeInfo?.loginImage) {
    if (typeof theme.themeInfo?.loginImage === 'string') {
      return theme.themeInfo?.loginImage
    } else {
      return URL.createObjectURL(theme.themeInfo?.loginImage)
    }
  } else {
    return ''
  }
})

const loginImage = computed(() => {
  if (theme.themeInfo?.loginImage) {
    return `${fileURL.value}`
  } else {
    const imgName = getThemeImg(theme.themeInfo?.theme)
    const imgPath = `${window.MaxKB.prefix}/theme/${imgName}.jpg`
    const imageUrl = new URL(imgPath, import.meta.url).href
    return imageUrl
  }
})
</script>
<style lang="scss" scoped>
.login-warp {
  height: 100vh;
  position: relative;
  overflow: hidden;
}

.login-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
}

.gradient-layer {
  position: absolute;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #fff5f0 0%, #ffe8d6 25%, #ffd4b8 50%, #ffe5d9 75%, #fff1e6 100%);
}

.decorative-shape {
  position: absolute;
  border-radius: 50%;
  opacity: 0.5;
  filter: blur(60px);
}

.shape-1 {
  width: 600px;
  height: 600px;
  background: linear-gradient(135deg, #ff9a56 0%, #ff6b35 100%);
  top: -200px;
  right: -100px;
  animation: float 20s ease-in-out infinite;
}

.shape-2 {
  width: 400px;
  height: 400px;
  background: linear-gradient(135deg, #ffd166 0%, #f4a261 100%);
  bottom: -100px;
  left: -100px;
  animation: float 15s ease-in-out infinite reverse;
}

.shape-3 {
  width: 300px;
  height: 300px;
  background: linear-gradient(135deg, #e76f51 0%, #ff6b6b 100%);
  top: 50%;
  left: 30%;
  animation: float 18s ease-in-out infinite;
}

.shape-4 {
  width: 250px;
  height: 250px;
  background: linear-gradient(135deg, #ffb4a2 0%, #ffcdb2 100%);
  bottom: 30%;
  right: 20%;
  animation: float 22s ease-in-out infinite reverse;
}

@keyframes float {
  0%, 100% {
    transform: translate(0, 0) scale(1);
  }
  33% {
    transform: translate(30px, -30px) scale(1.05);
  }
  66% {
    transform: translate(-20px, 20px) scale(0.95);
  }
}

.login-container {
  position: relative;
  z-index: 1;
}

.left-container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.login-hero {
  padding: 60px;
  position: relative;
  z-index: 2;
}

.hero-content {
  max-width: 500px;
}

.hero-title {
  font-size: 56px;
  font-weight: 800;
  background: linear-gradient(135deg, #e76f51 0%, #f4a261 50%, #ff6b35 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 20px;
  line-height: 1.2;
  text-shadow: 0 4px 20px rgba(255, 107, 53, 0.2);
}

.hero-subtitle {
  font-size: 20px;
  color: #665a4a;
  margin-bottom: 40px;
  font-weight: 500;
}

.hero-features {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.feature-item {
  display: flex;
  align-items: center;
  gap: 16px;
  padding: 16px 24px;
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(10px);
  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.8);
  transition: all 0.3s ease;
}

.feature-item:hover {
  transform: translateX(8px);
  background: rgba(255, 255, 255, 0.9);
  box-shadow: 0 8px 30px rgba(255, 107, 53, 0.15);
}

.feature-icon {
  font-size: 28px;
}

.feature-text {
  font-size: 18px;
  font-weight: 600;
  color: #5a4a3a;
}

.right-container {
  position: relative;
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(20px);
  border-left: 1px solid rgba(255, 255, 255, 0.5);
}

.right-container .lang {
  position: absolute;
  right: 24px;
  top: 24px;
  z-index: 10;
}

@media (max-width: 768px) {
  .hero-title {
    font-size: 36px;
  }

  .hero-subtitle {
    font-size: 16px;
  }

  .login-hero {
    padding: 30px;
  }
}
</style>
