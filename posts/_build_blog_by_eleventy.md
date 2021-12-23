---
title: Build Your Blog from Eleventy
description: This is a intro to build your blog by eleventy
date: 2021-11-17
tags:
  - posts
layout: layouts/post.njk
---
## [Note] Build Your Blog from Eleventy 

- 假如想要建置一個自己的blog
- 可以方便的使用Markdown語法
- 可以輕鬆的掛載到gihub.io上使用

那可以考慮看看`eleventy`這個架站套件，即使不太會前端的技能，也還是能蠻無痛的操作。
起源是一開始是從前端大神Huli分享一個post，是一個前端工程師分享關於 [為什麼我離開 Medium 用 eleventy 做一個 blog](https://jason-memo.dev/posts/why-i-leave-medium-and-build-blog-with-eleventy/)
其中分享了一個是Google AMP(Accelerated Mobile Page) tech lead所開發的[eleventy-high-performance-blog](https://github.com/google/eleventy-high-performance-blog) 

### 架站到github.io上步驟

1. 從Github 上 Fork [eleventy-high-performance-blog](https://github.com/google/eleventy-high-performance-blog)
    - 假如還沒有打算使用付費Github的話，Fork的Repo需要設為Public，假若是Private需要付費才可以設定為Pages。
2. 將Fork的Repo改名為 <github_username>.github.io 以便後續使用
3. Clone Repo下來修改些東西
    - `_data/metadata.json` ： 將其中的預設值改為自己的頁面資料
    - 於`posts/`資料夾中參考範例Markdown，可新增自己的頁面
    - 避免預設的test bench 影響到，可以先把 `test/test-generic-post.js`中的註解

4. 新增Github Action Deploy的設定，透過Github Action來在每次Pull後都會部署新的頁面
    - 於 `.github/workflows/build-and-test.yml`中新增以下
    ```text
        - name: Deploy
          uses: peaceiris/actions-gh-pages@v3
          with:
            publish_dir: ./_site
            github_token: ${{ secrets.GITHUB_TOKEN }}
    ```
5. 將新的更改Commit後Push到Repo
6. 從Github頁面設定Settings/Pages，將Source的select branch選為`gh-pages`，資料夾選擇`root`
    - 操作參考：https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
7.  修改後就能在`<github_username>.github.io`看到架設的靜態blog了！

## How to rebuild?
- Install dependency
```
$ npm install 
```
- Watch the demo page and edit at the same time
```
$ npm run watch 
```

## Resources
- [The language list support by eleventy](https://prismjs.com/#languages-list)
    - Example: show the python code at eleventy markdown
        ``` python 
    
        import librosa 
        
        class AudioProcessor(Object):
            """Define the AudioProcessor class.
            """
    
            def __init__(self, input_path: str, output_path: str):
                self.input_path = input_path
                self.output_path = output_path
            
        ``` 