---
title: "為 Digital Garden 新增留言功能"
created_at: 2023-10-13T02:43:00.631+08:00
published_at: 2023-10-13T02:43:04.282+08:00
tags:
---

在我之前的 Blog 是使用 Disqus 作為留言系統，但他讀取速度慢，且被買下來後就開始有些商業成份，管理留言也不方便，所以在架設 Digital Garden 時，我希望能順便換一個留言系統。

在我之前研究各個 Digital Garden 網站時，有看到一個是依賴於 GitHub 的留言系統實作，當時沒有記錄下來，但印象深刻。剛剛使用「GitHub 留言 blog」作為關鍵字去尋找時，看到 Nyo 寫的 [utterances: 使用 GitHub issue 做部落格的留言系統](https://nyogjtrc.github.io/posts/2021/03/utterances-use-github-issue-as-blog-comment-system/) 一文，滑到最下面看他的實際樣貌，對，就是這個！

透過這個方式，就能在靜態網站上也能擁有一個留言系統，而且又是透過開發者熟悉的 GitHub，我也很方便去管理。至於這樣會不會是一個留言門檻，我預期我的網站受眾主要還是以資訊社群為主，如果不會用 GitHub，或許我可以新增一個 Twitter 分享的按鈕，讓他分享時 mention 我去詢問。就我的經驗，其實會想留言的訪客其實不多，反倒是垃圾訊息會比較麻煩，權衡之下，用這樣的系統建構留言功能是一個好的方向。

但比較遺憾的是，留言的內容畢竟還是放在雲端上，會覺得資料不是掌握在自己手上有點不安與可惜。所以我預期會將好的留言，透過截圖的方式，另外存成筆記保留下來，這樣哪天我若又不得不換一個留言系統時，也能將這些好的內容留存。我也可以透過這個方式將 Disqus 的留言轉換到新網站上。

脈絡言至於此，就來實作看看吧！

到今天為止，是這樣的沒錯。但在拜訪了 [utterances](https://utteranc.es) 的官網後，發現已經有段時間沒有更新了，著實讓人有點擔心，所以就又嘗試找找看有沒有替代方案，於是就找到了受 [utterances](https://github.com/utterance/utterances) 啟發，並改用 [GitHub Discussions](https://docs.github.com/en/discussions) 驅動的留言系統—— [giscus](https://giscus.app)。

可以先來到其官網，他本身就附帶了一個套用程式碼的產生器，並有詳盡的說明引導你為要作為留言區的 Repository 做正確的設定，並協助驗證。

![[為 Digital Garden 新增留言功能-20231013014656715-CleanShot 2023-10-13 at 01.46.49@2x.png]]

經過一連串的選擇後，他會協助產生如下圖的程式碼：
![[為 Digital Garden 新增留言功能-20231013014824736-CleanShot 2023-10-13 at 01.47.55@2x.png]]

然而這樣的形式不一定適合直接套用在基於 Vue.js 的 Nuxt Content 上，萬幸的是他也有提供各大前端框架的元件使用，在 Vue.js 上的事 `@giscus/vue`，那就來安裝吧！

~~~shell
$ pnpm i @giscus/vue
~~~

先為這個套件提供的元件做一個 Adapter，建立 `@/components/Adapt/AdaptGiscus.vue`，其 Props 可以參照透過官網產生器所產出的 `data-` 屬性。

```vue
<template>
  <Giscus
      id="comments"
      repo="fntsrlike/local-garden"
      repoId="R_kgDOKfSl8Q"
      category="giscus"
      categoryId="DIC_kwDOKfSl8c4CaFL7"
      mapping="pathname"
      strict="0"
      reactionsEnabled="1"
      emitMetadata="0"
      inputPosition="top"
      :theme="theme"
      lang="zh-TW"
      loading="lazy"
    />
</template>
<script setup lang="ts">
import Giscus from '@giscus/vue'

const colorMode = useColorMode()
const theme = computed(() => `${colorMode.value}_protanopia` )
</script>
```


我預計會建立一個名為 `<PostMessageBoard />` 的元件放在 `@/components/Post/Page.vue` 的 `<article />` 下方。

```vue-html
<template>
  <article class="pb-4">
     <PostHeader :post="post"/>
     <PostContent :post="post"/>
     <PostFooter :post="post"/>
   </article>
   <PostMessageBoard />
</template>
```

接著來實作 `@/components/PostMessageBoard.vue`，算是避免未來要換留言系統時，可以只改一個地方的封裝。也可以在這邊寫一些期望留言遵守的規範。 

```html
<template>
  <section>
    <header>
      <h2 class="sr-only">Comments</h2>
    </header>
    <main>
      <AdaptGiscus />
    </main>
  </section>
</template>
<script setup lang="ts">
import AdaptGiscus from '../Adpat/AdaptGiscus.vue';
</script>
```
