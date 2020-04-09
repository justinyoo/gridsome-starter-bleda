<template>
  <Layout>
    <main>
      <header class="max-w-xl md:max-w-2xl xl:max-w-3xl mx-auto text-center px-6 pt-24">
        <h1 class="text-4xl sm:text-5xl md:text-6xl font-sans font-bold mb-1">Just in Chronicles</h1>
        <p class="text-grey-dark text-lg sm:text-3xl">Life as a Voyage</p>
      </header>
      <nav class="absolute top-0 left-0 z-20 mt-6 ml-6">
        <g-link to="/" class="text-gray-900 border-gray-400 text-sm border opacity-75 hover:opacity-100 rounded-full px-4 py-2 transition-opacity duration-300">&larr; Home</g-link>
      </nav>
      <article class="max-w-xl md:max-w-2xl xl:max-w-3xl mx-auto px-6 sm:px-12 pt-16 border-b border-gray-300 pb-10 mb-16">
        <div class="markdown text-lg leading-normal text-gray-700">
          <h2>My Talks</h2>
          <h3>2020</h3>
          <ol>
            <li>17/03/2020, <a href="https://aka.ms/GameStackLive" target="_blank">Game Stack Live</a> &ndash; <a href="https://youtu.be/oW-KCIJ-ph8" target="_blank">"From Code to Cloud: Streamlining your Development Workflow"</a></li>
            <li>03/02/2020, <a href="https://www.changbal.org/event-info/gaebalja-geulub-2wol-moim" target="_blank">Changbal: Korean IT Professional in Seattle Area</a> &ndash; <a href="https://github.com/justinyoo/blog/raw/dev/content/talks/20200203-changbal-github-actions-101.pdf" target="_blank">"GitHub Actions 101"</a></li>
            <li>22/01/2020, <a href="https://www.microsoft.com/ko-kr/ignite-the-tour/seoul" target="_blank">Ignite Tour Seoul</a> &ndash; <a href="https://github.com/justinyoo/blog/raw/dev/content/talks/20200122-mittseoul-afun70.pdf" target="_blank">"애저 리소스 사용 비용 절약하기"</a></li>
            <li>16/01/2020, <a href="https://conf.devopskorea.org/202001/" target="_blank">DevOps Korea</a> &ndash; <a href="https://github.com/justinyoo/blog/raw/dev/content/talks/20200116-devopskorea-github-actions-101.pdf" target="_blank">"깃헙 액션, 이것만 알면 참 쉽죠!"</a></li>
            <li>14/01/2020, <a href="https://www.microsoft.com/zh-cn/ignite-the-tour/shenzhen" target="_blank">Ignite Tour Shenzhen</a> &ndash; <a href="https://github.com/justinyoo/blog/raw/dev/content/talks/20200114-mittshenzhen-afun95.pdf" target="_blank">"清楚理解 Azure Functions 和 Azure 逻辑应用"</a></li>
          </ol>
        </div>
      </article>
      <site-footer class="pb-8 sm:pb-10" />
    </main>
  </Layout>
</template>

<script>
import config from '~/.temp/config.js'
import SiteFooter from '@/components/Footer'

export default {
  components: {
    SiteFooter
  },
  metaInfo () {
    return {
      title: 'About',
      meta: [
        {
          key: 'description',
          name: 'description',
          content: this.ogDescription
        },

        { property: "og:type", content: 'article' },
        { property: "og:title", content:'About' },
        { property: "og:description", content: this.ogDescription },
        { property: "og:url", content: `${this.config.siteUrl}/about/` },
        { property: "og:image", content: this.ogImageUrl },

        { name: "twitter:card", content: "summary_large_image" },
        { name: "twitter:title", content: 'About' },
        { name: "twitter:description", content: this.ogDescription },
        { name: "twitter:site", content: "@justinchronicle" },
        { name: "twitter:creator", content: "@justinchronicle" },
        { name: "twitter:image", content: this.ogImageUrl },
      ],
    }
  },
  computed: {
    config () {
      return config
    },
    ogDescription () {
      return 'Introduction to Just in Chronicle'
    },
    ogImageUrl () {
      return `${this.config.siteUrl}/images/twitter-card.png`
    }
  },
}
</script>
