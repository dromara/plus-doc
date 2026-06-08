<!-- _coverpage.md -->
<style>
  .cover-logo {
    display: block;
    width: 220px;
    width: min(42vw, 220px);
    max-width: 42vw;
    height: auto;
    margin: 0 auto 24px;
  }

  .cover-projects {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 32px 72px;
    max-width: 980px;
    width: min(100%, 980px);
    margin: 0 auto;
    text-align: center;
  }

  .cover-project {
    flex: 1 1 320px;
    max-width: 440px;
    min-width: 0;
    text-align: center;
  }

  .cover-title {
    margin: 0;
    font-size: 40px;
    font-size: clamp(26px, 6vw, 40px);
    font-weight: 700;
    line-height: 1.2;
    word-break: break-word;
  }

  .cover-subtitle {
    margin: 8px 0 20px;
    font-size: 36px;
    font-size: clamp(22px, 5vw, 36px);
    font-weight: 700;
    line-height: 1.25;
    word-break: keep-all;
  }

  .cover-badges {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    gap: 8px;
  }

  .cover-badges img {
    max-width: 100%;
    height: auto;
    vertical-align: middle;
  }

  section.cover {
    justify-content: center;
  }

  section.cover .cover-main {
    box-sizing: border-box;
    flex: 0 1 1120px;
    width: 100%;
    max-width: 1120px;
    margin: 0 auto;
    padding: 24px 12px;
    text-align: center;
  }

  section.cover blockquote {
    max-width: 760px;
    margin: 28px auto 0;
    padding: 0 12px;
    font-size: 24px;
    font-size: clamp(17px, 4vw, 24px);
    line-height: 1.8;
  }

  @media screen and (max-width: 640px) {
    .cover-logo {
      width: 128px;
      max-width: 38vw;
      margin-bottom: 18px;
    }

    .cover-projects {
      gap: 24px;
    }

    .cover-project {
      flex-basis: 100%;
    }

    .cover-subtitle {
      margin-bottom: 14px;
    }

    section.cover p {
      margin: 0.8em 0;
    }

    section.cover .cover-main > p:last-child a {
      width: min(100%, 260px);
      margin: 0.35rem auto;
      padding: 0.7em 1.2rem;
      letter-spacing: 0;
    }
  }
</style>

<img class="cover-logo" src="static/image/logo.png" alt="RuoYi-Plus Logo">

<div class="cover-projects">
  <div class="cover-project">
    <div class="cover-title">RuoYi-Vue-Plus</div>
    <div class="cover-subtitle">通用权限管理系统</div>
    <div class="cover-badges">
      <a href="https://gitee.com/dromara/RuoYi-Vue-Plus"><img src="https://gitee.com/dromara/RuoYi-Vue-Plus/badge/star.svg?theme=blue" alt="码云Gitee"></a>
      <a href="https://github.com/dromara/RuoYi-Vue-Plus"><img src="https://img.shields.io/github/stars/dromara/RuoYi-Vue-Plus?style=social&amp;label=Github%20Stars" alt="GitHub Stars"></a>
      <a href="https://gitcode.com/dromara/RuoYi-Vue-Plus"><img src="https://gitcode.com/dromara/RuoYi-Vue-Plus/star/badge.svg" alt="GitCode Star"></a>
      <a href="https://gitee.com/dromara/RuoYi-Vue-Plus/blob/master/LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License MIT"></a>
      <a href="https://gitee.com/dromara/RuoYi-Vue-Plus"><img src="https://img.shields.io/badge/RuoYi_Vue_Plus-5.6.1-success.svg" alt="RuoYi-Vue-Plus 5.6.1"></a>
      <img src="https://img.shields.io/badge/Spring%20Boot-3.5-blue.svg" alt="Spring Boot 3.5">
    </div>
  </div>

  <div class="cover-project">
    <div class="cover-title">RuoYi-Cloud-Plus</div>
    <div class="cover-subtitle">微服务权限管理系统</div>
    <div class="cover-badges">
      <a href="https://gitee.com/dromara/RuoYi-Cloud-Plus"><img src="https://gitee.com/dromara/RuoYi-Cloud-Plus/badge/star.svg?theme=blue" alt="码云Gitee"></a>
      <a href="https://github.com/dromara/RuoYi-Cloud-Plus"><img src="https://img.shields.io/github/stars/dromara/RuoYi-Cloud-Plus?style=social&amp;label=Github%20Stars" alt="GitHub Stars"></a>
      <a href="https://gitcode.com/dromara/RuoYi-Cloud-Plus"><img src="https://gitcode.com/dromara/RuoYi-Cloud-Plus/star/badge.svg" alt="GitCode Star"></a>
      <a href="https://gitee.com/dromara/RuoYi-Cloud-Plus/blob/master/LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License MIT"></a>
      <a href="https://gitee.com/dromara/RuoYi-Cloud-Plus"><img src="https://img.shields.io/badge/RuoYi_Cloud_Plus-2.6.1-success.svg" alt="RuoYi-Cloud-Plus 2.6.1"></a>
      <img src="https://img.shields.io/badge/Spring%20Boot-3.5-blue.svg" alt="Spring Boot 3.5">
    </div>
  </div>
</div>

> 💪真正面向企业级的应用框架
>
> 组件化 模块化 轻耦合 高扩展 针对企业痛点 业界一流技术栈

Copyright © 2018-2026 疯狂的狮子Li All Rights Reserved.

[开始使用 Let's Go](/6.X/_readme.md)
