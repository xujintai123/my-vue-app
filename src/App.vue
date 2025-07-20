<template>
  <div id="app">
    <!-- 导航栏 -->
    <nav class="navbar" :class="{ 'navbar-scrolled': scrolled }">
      <div class="nav-container">
        <div class="nav-logo">
          <span class="logo-text">xu jintai</span>
        </div>
        <div class="nav-links">
          <a href="#home" @click="scrollToSection('home')">首页</a>
          <a href="#about" @click="scrollToSection('about')">关于</a>
          <a href="#skills" @click="scrollToSection('skills')">技能</a>
          <a href="#projects" @click="scrollToSection('projects')">项目</a>
          <a href="#contact" @click="scrollToSection('contact')">联系</a>
        </div>
        <div class="nav-toggle" @click="toggleMobileMenu">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
    </nav>

    <!-- 英雄区域 -->
    <section id="home" class="hero">
      <div class="hero-bg">
        <div class="floating-shapes">
          <div class="shape shape-1"></div>
          <div class="shape shape-2"></div>
          <div class="shape shape-3"></div>
          <div class="shape shape-4"></div>
        </div>
      </div>
      <div class="hero-content">
        <h1 class="hero-title">
          <span class="title-line">欢迎来到</span>
          <span class="title-line highlight">xujintai 的世界</span>
        </h1>
        <p class="hero-description">
          {{ typedText }}<span class="cursor" :class="{ 'blink': showCursor }">|</span>
        </p>
        <div class="hero-buttons">
          <button class="btn btn-primary" @click="scrollToSection('projects')">
            查看项目
          </button>
          <button class="btn btn-secondary" @click="scrollToSection('contact')">
            联系我
          </button>
        </div>
      </div>
    </section>

    <!-- 关于我 -->
    <section id="about" class="about">
      <div class="container">
        <h2 class="section-title">关于我</h2>
        <div class="about-content">
          <div class="about-text">
            <p>我是一名充满激情的前端开发者，专注于创建美观且实用的网络应用。</p>
            <p>拥有丰富的Vue.js、React和现代JavaScript开发经验。</p>
            <div class="stats">
              <div class="stat-item">
                <span class="stat-number">{{ projectCount }}</span>
                <span class="stat-label">项目完成</span>
              </div>
              <div class="stat-item">
                <span class="stat-number">{{ experienceYears }}</span>
                <span class="stat-label">年经验</span>
              </div>
              <div class="stat-item">
                <span class="stat-number">{{ clientsServed }}</span>
                <span class="stat-label">客户服务</span>
              </div>
            </div>
          </div>
          <div class="about-image">
            <div class="image-placeholder">
              <div class="pulse-ring"></div>
              <div class="avatar">👨‍💻</div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 技能 -->
    <section id="skills" class="skills">
      <div class="container">
        <h2 class="section-title">技能专长</h2>
        <div class="skills-grid">
          <div class="skill-card" v-for="skill in skills" :key="skill.name">
            <div class="skill-icon">{{ skill.icon }}</div>
            <h3 class="skill-name">{{ skill.name }}</h3>
            <div class="skill-progress">
              <div class="progress-bar" :style="{ width: skill.level + '%' }"></div>
            </div>
            <span class="skill-level">{{ skill.level }}%</span>
          </div>
        </div>
      </div>
    </section>

    <!-- 项目 -->
    <section id="projects" class="projects">
      <div class="container">
        <h2 class="section-title">精选项目</h2>
        <div class="projects-grid">
          <div class="project-card" v-for="project in projects" :key="project.id">
            <div class="project-image">
              <div class="project-overlay">
                <div class="project-links">
                  <a href="#" class="project-link">🔗 演示</a>
                  <a href="#" class="project-link">📱 代码</a>
                </div>
              </div>
            </div>
            <div class="project-content">
              <h3 class="project-title">{{ project.title }}</h3>
              <p class="project-description">{{ project.description }}</p>
              <div class="project-tech">
                <span class="tech-tag" v-for="tech in project.technologies" :key="tech">
                  {{ tech }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 联系我 -->
    <section id="contact" class="contact">
      <div class="container">
        <h2 class="section-title">联系我</h2>
        <div class="contact-content">
          <div class="contact-info">
            <div class="contact-item">
              <div class="contact-icon">📧</div>
              <div class="contact-details">
                <h3>邮箱</h3>
                <p>x**@163.com</p>
              </div>
            </div>
            <div class="contact-item">
              <div class="contact-icon">📱</div>
              <div class="contact-details">
                <h3>电话</h3>
                <p>+86 1** 0000 0000</p>
              </div>
            </div>
            <div class="contact-item">
              <div class="contact-icon">📍</div>
              <div class="contact-details">
                <h3>地址</h3>
                <p>中国，上海</p>
              </div>
            </div>
          </div>
          <form class="contact-form" @submit.prevent="submitForm">
            <div class="form-group">
              <input type="text" v-model="form.name" placeholder="您的姓名" required>
            </div>
            <div class="form-group">
              <input type="email" v-model="form.email" placeholder="您的邮箱" required>
            </div>
            <div class="form-group">
              <textarea v-model="form.message" placeholder="您的留言" rows="4" required></textarea>
            </div>
            <button type="submit" class="btn btn-primary">
              {{ formSubmitting ? '发送中...' : '发送消息' }}
            </button>
          </form>
        </div>
      </div>
    </section>

    <!-- 页脚 -->
    <footer class="footer">
      <div class="container">
        <p>&copy; {{ currentFullYear }} xujintai. 保留所有权利.</p>
        <div class="social-links">
          <a href="#" class="social-link">GitHub</a>
          <a href="#" class="social-link">LinkedIn</a>
          <a href="#" class="social-link">Twitter</a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      scrolled: false,
      showCursor: true,
      typedText: '',
      fullText: '全栈开发者 | Vue.js专家 | 创意实现者',
      typeIndex: 0,
      projectCount: 0,
      experienceYears: 0,
      clientsServed: 0,
      formSubmitting: false,
      currentFullYear: new Date().getFullYear(),
      form: {
        name: '',
        email: '',
        message: ''
      },
      skills: [
        { name: 'Vue.js', level: 95, icon: '🟢' },
        { name: 'JavaScript', level: 90, icon: '🟡' },
        { name: 'HTML5', level: 95, icon: '🔴' },
        { name: 'CSS3', level: 90, icon: '🔵' },
        { name: 'Node.js', level: 85, icon: '🟢' },
        { name: 'React', level: 80, icon: '🔵' }
      ],
      projects: [
        {
          id: 1,
          title: '企业管理系统',
          description: '基于Vue.js的现代化企业管理系统，支持多角色权限管理。',
          technologies: ['Vue.js', 'Element UI', 'Node.js', 'MongoDB']
        },
        {
          id: 2,
          title: '电商平台',
          description: '响应式电商平台，包含购物车、支付集成和订单管理。',
          technologies: ['Vue.js', 'Vuex', 'Express', 'MySQL']
        },
        {
          id: 3,
          title: '数据可视化大屏',
          description: '实时数据可视化展示系统，支持多种图表类型。',
          technologies: ['Vue.js', 'ECharts', 'WebSocket', 'Redis']
        }
      ]
    }
  },
  mounted() {
    this.handleScroll()
    this.typeWriter()
    this.animateStats()
    window.addEventListener('scroll', this.handleScroll)
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll() {
      this.scrolled = window.scrollY > 50
    },
    scrollToSection(sectionId) {
      const element = document.getElementById(sectionId)
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' })
      }
    },
    toggleMobileMenu() {
      // 移动端菜单切换逻辑
      console.log('Toggle mobile menu')
    },
    typeWriter() {
      if (this.typeIndex < this.fullText.length) {
        this.typedText += this.fullText.charAt(this.typeIndex)
        this.typeIndex++
        setTimeout(this.typeWriter, 50)
      } else {
        setInterval(() => {
          this.showCursor = !this.showCursor
        }, 500)
      }
    },
    animateStats() {
      this.animateNumber('projectCount', 50, 2000)
      this.animateNumber('experienceYears', this.currentFullYear - 2021, 1500)
      this.animateNumber('clientsServed', 20, 2500)
    },
    animateNumber(property, target, duration) {
      const start = 0
      const startTime = Date.now()
      const timer = setInterval(() => {
        const elapsed = Date.now() - startTime
        const progress = Math.min(elapsed / duration, 1)
        this[property] = Math.floor(start + (target - start) * progress)
        if (progress >= 1) {
          clearInterval(timer)
        }
      }, 16)
    },
    submitForm() {
      this.formSubmitting = true
      // 模拟表单提交
      setTimeout(() => {
        this.formSubmitting = false
        alert('消息已发送！')
        this.form = { name: '', email: '', message: '' }
      }, 1000)
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  line-height: 1.6;
  color: #333;
  overflow-x: hidden;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* 导航栏 */
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  z-index: 1000;
  transition: all 0.3s ease;
}

.navbar-scrolled {
  background: rgba(255, 255, 255, 0.98);
  box-shadow: 0 2px 20px rgba(0, 0, 0, 0.1);
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 70px;
}

.logo-text {
  font-size: 24px;
  font-weight: bold;
  background: linear-gradient(45deg, #667eea, #764ba2);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.nav-links {
  display: flex;
  gap: 30px;
}

.nav-links a {
  text-decoration: none;
  color: #333;
  font-weight: 500;
  position: relative;
  transition: color 0.3s ease;
}

.nav-links a::after {
  content: '';
  position: absolute;
  width: 0;
  height: 2px;
  bottom: -5px;
  left: 0;
  background: linear-gradient(45deg, #667eea, #764ba2);
  transition: width 0.3s ease;
}

.nav-links a:hover::after {
  width: 100%;
}

.nav-toggle {
  display: none;
  flex-direction: column;
  cursor: pointer;
}

.nav-toggle span {
  width: 25px;
  height: 3px;
  background: #333;
  margin: 3px 0;
  transition: 0.3s;
}

/* 英雄区域 */
.hero {
  position: relative;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  z-index: -1;
}

.floating-shapes {
  position: absolute;
  width: 100%;
  height: 100%;
}

.shape {
  position: absolute;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.1);
  animation: float 6s ease-in-out infinite;
}

.shape-1 {
  width: 80px;
  height: 80px;
  top: 20%;
  left: 10%;
  animation-delay: 0s;
}

.shape-2 {
  width: 120px;
  height: 120px;
  top: 60%;
  right: 15%;
  animation-delay: 2s;
}

.shape-3 {
  width: 60px;
  height: 60px;
  bottom: 30%;
  left: 20%;
  animation-delay: 4s;
}

.shape-4 {
  width: 100px;
  height: 100px;
  top: 10%;
  right: 30%;
  animation-delay: 1s;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(180deg); }
}

.hero-content {
  text-align: center;
  color: white;
  z-index: 1;
}

.hero-title {
  font-size: 3.5rem;
  margin-bottom: 1rem;
  line-height: 1.2;
}

.title-line {
  display: block;
  opacity: 0;
  animation: slideInUp 0.8s ease forwards;
}

.title-line:nth-child(2) {
  animation-delay: 0.3s;
}

.highlight {
  background: linear-gradient(45deg, #ffd700, #ffed4e);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-description {
  font-size: 1.5rem;
  margin-bottom: 2rem;
  opacity: 0;
  animation: slideInUp 0.8s ease forwards;
  animation-delay: 0.6s;
}

.cursor {
  animation: blink 1s infinite;
}

.cursor.blink {
  opacity: 0;
}

@keyframes blink {
  0%, 50% { opacity: 1; }
  51%, 100% { opacity: 0; }
}

.hero-buttons {
  display: flex;
  gap: 20px;
  justify-content: center;
  opacity: 0;
  animation: slideInUp 0.8s ease forwards;
  animation-delay: 0.9s;
}

@keyframes slideInUp {
  from {
    opacity: 0;
    transform: translateY(50px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* 按钮样式 */
.btn {
  padding: 12px 30px;
  border: none;
  border-radius: 50px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  text-decoration: none;
  display: inline-block;
}

.btn-primary {
  background: linear-gradient(45deg, #667eea, #764ba2);
  color: white;
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(102, 126, 234, 0.4);
}

.btn-secondary {
  background: transparent;
  color: white;
  border: 2px solid white;
}

.btn-secondary:hover {
  background: white;
  color: #667eea;
  transform: translateY(-2px);
}

/* 通用区域样式 */
.section-title {
  font-size: 2.5rem;
  text-align: center;
  margin-bottom: 3rem;
  background: linear-gradient(45deg, #667eea, #764ba2);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* 关于我 */
.about {
  padding: 80px 0;
  background: #f8f9fa;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
}

.about-text p {
  font-size: 1.1rem;
  margin-bottom: 1.5rem;
  color: #666;
}

.stats {
  display: flex;
  gap: 30px;
  margin-top: 2rem;
}

.stat-item {
  text-align: center;
}

.stat-number {
  display: block;
  font-size: 2.5rem;
  font-weight: bold;
  color: #667eea;
}

.stat-label {
  font-size: 0.9rem;
  color: #666;
}

.about-image {
  display: flex;
  justify-content: center;
}

.image-placeholder {
  position: relative;
  width: 200px;
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.pulse-ring {
  position: absolute;
  width: 100%;
  height: 100%;
  border: 3px solid #667eea;
  border-radius: 50%;
  animation: pulse-ring 2s ease-in-out infinite;
}

@keyframes pulse-ring {
  0% {
    transform: scale(0.8);
    opacity: 1;
  }
  100% {
    transform: scale(1.2);
    opacity: 0;
  }
}

.avatar {
  font-size: 4rem;
  background: linear-gradient(45deg, #667eea, #764ba2);
  width: 150px;
  height: 150px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* 技能 */
.skills {
  padding: 80px 0;
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 30px;
}

.skill-card {
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
  text-align: center;
  transition: transform 0.3s ease;
}

.skill-card:hover {
  transform: translateY(-5px);
}

.skill-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.skill-name {
  font-size: 1.2rem;
  margin-bottom: 1rem;
  color: #333;
}

.skill-progress {
  width: 100%;
  height: 8px;
  background: #e9ecef;
  border-radius: 10px;
  overflow: hidden;
  margin-bottom: 0.5rem;
}

.progress-bar {
  height: 100%;
  background: linear-gradient(45deg, #667eea, #764ba2);
  border-radius: 10px;
  transition: width 2s ease;
}

.skill-level {
  font-size: 0.9rem;
  color: #666;
  font-weight: 600;
}

/* 项目 */
.projects {
  padding: 80px 0;
  background: #f8f9fa;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 30px;
}

.project-card {
  background: white;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.project-card:hover {
  transform: translateY(-5px);
}

.project-image {
  height: 200px;
  background: linear-gradient(45deg, #667eea, #764ba2);
  position: relative;
  overflow: hidden;
}

.project-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.project-card:hover .project-overlay {
  opacity: 1;
}

.project-links {
  display: flex;
  gap: 15px;
}

.project-link {
  color: white;
  text-decoration: none;
  padding: 8px 15px;
  border: 2px solid white;
  border-radius: 20px;
  transition: all 0.3s ease;
}

.project-link:hover {
  background: white;
  color: #667eea;
}

.project-content {
  padding: 25px;
}

.project-title {
  font-size: 1.3rem;
  margin-bottom: 1rem;
  color: #333;
}

.project-description {
  color: #666;
  margin-bottom: 1.5rem;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.tech-tag {
  background: linear-gradient(45deg, #667eea, #764ba2);
  color: white;
  padding: 4px 12px;
  border-radius: 15px;
  font-size: 0.8rem;
}

/* 联系我 */
.contact {
  padding: 80px 0;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-bottom: 30px;
}

.contact-icon {
  font-size: 2rem;
  width: 60px;
  height: 60px;
  background: linear-gradient(45deg, #667eea, #764ba2);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.contact-details h3 {
  margin-bottom: 5px;
  color: #333;
}

.contact-details p {
  color: #666;
}

.contact-form {
  background: white;
  padding: 40px;
  border-radius: 15px;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
}

.form-group {
  margin-bottom: 20px;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 15px;
  border: 2px solid #e9ecef;
  border-radius: 10px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #667eea;
}

/* 页脚 */
.footer {
  background: #333;
  color: white;
  padding: 40px 0;
  text-align: center;
}

.footer .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.social-links {
  display: flex;
  gap: 20px;
}

.social-link {
  color: white;
  text-decoration: none;
  transition: color 0.3s ease;
}

.social-link:hover {
  color: #667eea;
}

/* 响应式设计 */
@media (max-width: 768px) {
  .nav-links {
    display: none;
  }
  
  .nav-toggle {
    display: flex;
  }
  
  .hero-title {
    font-size: 2.5rem;
  }
  
  .hero-description {
    font-size: 1.2rem;
  }
  
  .hero-buttons {
    flex-direction: column;
    align-items: center;
  }
  
  .about-content,
  .contact-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .stats {
    justify-content: center;
  }
  
  .skills-grid,
  .projects-grid {
    grid-template-columns: 1fr;
  }
  
  .footer .container {
    flex-direction: column;
    gap: 20px;
  }
}
</style>
