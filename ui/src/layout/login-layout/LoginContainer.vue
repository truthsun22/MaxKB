<template>
  <div class="login-form-container">
    <div class="login-card-wrapper">
      <div class="login-card-header">
        <div class="logo-wrapper">
          <div class="logo-icon">
            <span class="logo-text">R</span>
          </div>
        </div>
        <h2 class="login-title" v-if="loginTitle">{{ loginTitle }}</h2>
        <p class="login-subtitle" v-if="subTitle">{{ subTitle }}</p>
      </div>
      <div class="login-card-body">
        <slot></slot>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  title: String,
  subTitle: String,
})

const loginTitle = computed(() => {
  return props.title || undefined
})
</script>
<style lang="scss" scoped>
.login-form-container {
  width: 100%;
  max-width: 420px;
  padding: 24px;
}

.login-card-wrapper {
  background: rgba(255, 255, 255, 0.95);
  border-radius: 24px;
  box-shadow: 
    0 8px 32px rgba(255, 107, 53, 0.1),
    0 2px 8px rgba(255, 107, 53, 0.05);
  overflow: hidden;
  position: relative;
}

.login-card-wrapper::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: linear-gradient(90deg, #ff6b35, #f4a261, #e76f51, #ff6b35);
  background-size: 200% 100%;
  animation: gradientMove 3s ease infinite;
}

@keyframes gradientMove {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.login-card-header {
  padding: 40px 32px 32px;
  text-align: center;
}

.logo-wrapper {
  margin-bottom: 20px;
  display: flex;
  justify-content: center;
}

.logo-icon {
  width: 72px;
  height: 72px;
  border-radius: 20px;
  background: linear-gradient(135deg, #ff6b35 0%, #f4a261 50%, #e76f51 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 
    0 8px 24px rgba(255, 107, 53, 0.3),
    inset 0 2px 4px rgba(255, 255, 255, 0.3);
  position: relative;
}

.logo-icon::before {
  content: '';
  position: absolute;
  top: 4px;
  left: 4px;
  right: 4px;
  bottom: 4px;
  border-radius: 16px;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.2) 0%, rgba(255, 255, 255, 0) 50%);
}

.logo-text {
  font-size: 36px;
  font-weight: 800;
  color: white;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  position: relative;
  z-index: 1;
}

.login-title {
  font-size: 28px;
  font-weight: 700;
  color: #3d2b1f;
  margin: 0 0 8px 0;
  background: linear-gradient(135deg, #e76f51, #f4a261);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.login-subtitle {
  font-size: 14px;
  color: #8b7355;
  margin: 0;
  font-weight: 400;
}

.login-card-body {
  padding: 0 32px 40px;
}

.login-form {
  width: 100%;
}

:deep(.el-input__wrapper) {
  background: #fff9f5;
  border: 1px solid #ffe4d6;
  border-radius: 12px;
  padding: 12px 16px;
  transition: all 0.3s ease;
  box-shadow: none;
}

:deep(.el-input__wrapper:hover) {
  border-color: #ffb99a;
  background: #fff5ef;
}

:deep(.el-input__wrapper.is-focus) {
  border-color: #ff6b35;
  box-shadow: 0 0 0 3px rgba(255, 107, 53, 0.1);
  background: #ffffff;
}

:deep(.el-input__inner) {
  font-size: 15px;
  color: #3d2b1f;
}

:deep(.el-input__inner::placeholder) {
  color: #bfa893;
}

:deep(.el-button--primary) {
  background: linear-gradient(135deg, #ff6b35 0%, #f4a261 100%);
  border: none;
  border-radius: 12px;
  padding: 14px 24px;
  font-size: 16px;
  font-weight: 600;
  height: auto;
  transition: all 0.3s ease;
  box-shadow: 0 4px 12px rgba(255, 107, 53, 0.3);
}

:deep(.el-button--primary:hover) {
  background: linear-gradient(135deg, #e7602e 0%, #e89657 100%);
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(255, 107, 53, 0.4);
}

:deep(.el-button--primary:active) {
  transform: translateY(0);
  box-shadow: 0 2px 8px rgba(255, 107, 53, 0.3);
}

:deep(.el-button--primary.is-loading) {
  background: linear-gradient(135deg, #ff6b35 0%, #f4a261 100%);
}

:deep(.el-button--text) {
  color: #ff6b35;
  font-size: 14px;
  font-weight: 500;
}

:deep(.el-button--text:hover) {
  color: #e7602e;
  background: rgba(255, 107, 53, 0.05);
}

:deep(.el-card) {
  border: none;
  box-shadow: none;
  background: transparent;
}

:deep(.el-card__body) {
  padding: 0;
}

:deep(.mb-24) {
  margin-bottom: 24px !important;
}

:deep(.mb-12) {
  margin-bottom: 12px !important;
}

:deep(.mt-12) {
  margin-top: 12px !important;
}

:deep(.mt-16) {
  margin-top: 16px !important;
}

:deep(.mt-24) {
  margin-top: 24px !important;
}

:deep(.ml-8) {
  margin-left: 8px !important;
}

:deep(.flex-between) {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

:deep(.w-full) {
  width: 100%;
}

:deep(.text-center) {
  text-align: center;
}

:deep(.input-item) {
  width: 100%;
}

:deep(.operate-container) {
  margin-top: 12px;
}

:deep(.forgot-password) {
  padding: 0;
  margin: 0;
}

:deep(.login-gradient-divider) {
  position: relative;
  text-align: center;
  color: #bfa893;
  font-size: 13px;
  margin: 24px 0;
}

:deep(.login-gradient-divider::before) {
  content: '';
  width: 25%;
  height: 1px;
  background: linear-gradient(90deg, transparent, #ffe4d6);
  position: absolute;
  left: 16px;
  top: 50%;
}

:deep(.login-gradient-divider::after) {
  content: '';
  width: 25%;
  height: 1px;
  background: linear-gradient(90deg, #ffe4d6, transparent);
  position: absolute;
  right: 16px;
  top: 50%;
}

:deep(.login-button-circle) {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  border: 1px solid #ffe4d6;
  background: #fff9f5;
  transition: all 0.3s ease;
  padding: 0 !important;
  margin: 0 6px;
}

:deep(.login-button-circle:hover) {
  border-color: #ff6b35;
  background: #fff5ef;
  transform: scale(1.05);
}

:deep(.color-secondary) {
  color: #ff6b35;
}

@media (max-width: 768px) {
  .login-form-container {
    padding: 16px;
  }

  .login-card-header {
    padding: 32px 24px 24px;
  }

  .login-card-body {
    padding: 0 24px 32px;
  }

  .login-title {
    font-size: 24px;
  }

  .logo-icon {
    width: 64px;
    height: 64px;
  }

  .logo-text {
    font-size: 32px;
  }
}
</style>
