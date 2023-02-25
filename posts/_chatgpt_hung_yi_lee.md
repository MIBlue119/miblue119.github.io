---
title: 20230225 Hung-yi Lee 台大李宏毅教授分享 ChatGPT原理
description: This is a summary of a NTU professor's speech
date: 2023-02-25
tags:
  - gpt
layout: layouts/post.njk
---
科普_20230225 Hung-yi Lee 台大李宏毅教授分享 ChatGPT原理


- [原理剖析 (1/3) — 對 ChatGPT 的常見誤解](https://www.youtube.com/watch?v=yiY4nPOzJEg)
	- 一個具備很多(175Billion)參數的模型，可以看成一個方程式，會根據使用者輸入的文字，進行文字接龍。他會從很多字中挑出機率最高的接，後續的輸出也會根據前面的接龍結果，再找出機率最高的字詞接上去。
	- open AI的工程師透過網路搜集的大量資料，去找出那個方程式。
- [原理剖析(2/3) - 預訓練(Pre-train)](https://www.youtube.com/watch?v=1ah7Qsri_c8&t=15s)
	- GPT的全名是 Generative Pretrained Transformer
		- 其中的基礎架構是來自2017 Google的  [Attention Is All You Need](https://arxiv.org/pdf/1706.03762.pdf)
			- 論文中提到self attention的學習機制，可以學習序列資料的短距離/長距離關係。
	- 一般的AI訓練，透過督導式學習，人類提供問題與正確答案訓練資料，找到那個可以符合規則的function。但假如當輸入資料/問題，超過他的訓練資料範圍，他就會爛掉。而成對的問題與正確答案資料，取得的成本高，需要有人/專家花時間確認答案的正確性，而數量也會有限。
	- 有沒有什麼方式，可以無痛產生成對資料？
		- 把網路上的每一段文字，來讓機器文字接龍。
			- 例如：一段句子『世界第一高峰是喜馬拉雅山』，我們拆成前後段。前段『世界第一高峰是』當做輸入，而後段『喜馬拉雅山』不管是不是正確的敘述，都告訴機器是正確的，讓他自己去找到fuction，可以讓輸出的第一個字機率更接近『喜』
	- GPT的歷史
		- 2018 GPT 參數量117M，當時用到的訓練資料是1GB
		- 2019 GPT2 參數量1542M，訓練資料變為40GB
			- 開始具備回答QA能力，在一個QA的資料集中，當時正確率隨著參數成長也有成長，60%的正確率(人類90%)
		- 2020 GPT3 參數量175 Billion，原本有45TB的資料，經過filtering訓練資料是570GB
			- 訓練資料有來自Github(程式託管平台)的程式，因此可以應對程式接龍。
			- 在42個任務上有50個％的正確率，當時的人覺得這麼大的參數量卻表現不符合期待/不受控。
			- 能怎麼處理這個狀況？ chatGPT的產生
				- 前面提到GPT透過一堆大量資料，透過文字接龍的方式學習。我們使用無痛的方式生成了成對的訓練資料，讓機器自督導學習(Self supervised learning)，那個階段我們稱之為預訓練(pretrained)。那階段得到的模型，我們稱呼為基石模型(foundation model)
					- 預訓練的幫助？
						- 在多種語言上的文字接龍後，只要教某一個語言的某一個任務，就能自動學會其他語言的同樣任務。例如教了學習英文閱讀能力測驗，也能學會在中文閱讀能力測驗。
				- chatGPT的產生
					- 督導式學習：是再透過人類老師提供的正確資料微調，不過這樣人類老師也還是很辛苦，因此有下個方式的學習。
					- 增強式學習：透過PPO(Proximal Policy Optimization)算法，不是直接給答案，人類老師是針對GPT的答案給予讚/噓。可以節省人類的力量，或是應對不太確定正確答案的生成結果。
- [原理剖析(3/3)-ChatGPT所帶來的研究問題](https://www.youtube.com/watch?v=UsaZhQ9bY2k)
	- slide: https://drive.google.com/file/d/1wRxoj0xxXfe2MtcX1D8BbTE1IKbzUg5j/view 
	- 怎麼讓chatGPT不會亂回答？
		- 精準提出需求，對chatGTP進行『催眠』，在學術界叫做Prompting
			- 網路上有不少相關鄉民整理
				- https://github.com/PlexPt/awesome-chatgpt-prompts-zh 
				- https://www.rayskyinvest.com/96682/chatgpt-examples
				- https://www.explainthis.io/zh-hant/chatgpt/website
	- chatGTP使用的訓練資料只到2021，要如何更新他呢？
		- 要如何更新一個錯誤的回答，但不會把其他部份搞爛？
			- 新的題目：『Neural Editing』
	- 如何偵測人工智慧生成的物件？文字/聲音/影像
	- 如何讓chatGPT不會洩漏隱私資料？『Machine Unlearning』，讓機器忘記他曾經學過的資訊
  
 <!-- ## Section Header

<a href="{{ '/posts/firstpost/' | url }}">First post</a>
<a href="{{ '/posts/thirdpost/' | url }}">Third post</a>

Bring to the table win-win survival strategies to ensure proactive domination. At the end of the day, going forward, a new normal that has evolved from generation X is on the runway heading towards a streamlined cloud solution. User generated content in real-time will have multiple touchpoints for offshoring.

Capitalize on low hanging fruit to identify a ballpark value added activity to beta test. Override the digital divide with additional clickthroughs from DevOps. Nanotechnology immersion along the information highway will close the loop on focusing solely on the bottom line.

# Test SVG

![Test Share SVG](/img/share.svg)

# Test Relative Local Image

![Test Share SVG](../../img/doener.jpg) -->
