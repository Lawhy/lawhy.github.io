---
title: "Open Source for LLM Post-Training: What Can We Build?"
date: 2026-10-22
slug: oss-post-training
summary: ""
authors: '<a href="https://www.yuanhe.wiki/">Yuan He</a>'
comments: true
---

<aside class="post-aside">
<h3>Resources</h3>
<ul>
  <li><img class="favicon" src="https://www.google.com/s2/favicons?domain=arxiv.org&sz=32" alt=""><a href="https://arxiv.org/abs/2609.29421">Rufus-Air paper</a></li>
  <li><img class="favicon" src="https://www.google.com/s2/favicons?domain=linkedin.com&sz=32" alt=""><a href="https://lnkd.in/p/gCrMgaTJ">LinkedIn post</a></li>
  <li><img class="favicon" src="https://www.google.com/s2/favicons?domain=x.com&sz=32" alt=""><a href="https://x.com/tourzhao/status/2110512117183094810">X post</a></li>
  <li><img class="favicon" src="https://www.google.com/s2/favicons?domain=github.com&sz=32" alt=""><a href="https://github.com/Lawhy/tokin">Lawhy/tokin</a></li>
</ul>
</aside>

A lightning talk given at [Open Infra Night for Agent Builders](https://luma.com/jsu2t3ad), part of Open Source AI Week in San Francisco. It asks how far a small team can take a base model with open-source resources alone. Our answer is [Rufus-Air](https://arxiv.org/abs/2609.29421), a post-training effort at Amazon Rufus led by Tuo Zhao: an open recipe on GLM-4.5-Air-Base with eight serial stages, from hard rewards to soft ones, built on slime, Megatron-LM, SGLang and Strands Agents. The talk then zooms into the harness stack behind its agentic stages, the small details that silently break agentic RL, and finally introduces [tokin](https://github.com/Lawhy/tokin), an open-source gateway that makes any agent harness token-native...

<div class="post-deck">
  <iframe class="post-deck__frame" src="slides/deck.html" title="Open Source for LLM Post-Training: What Can We Build? — slides" allowfullscreen></iframe>
</div>

<div class="post-deck__bar">
  <span class="post-deck__hint">Click left / right to navigate &middot; <kbd>1</kbd> &rarr; first slide.</span>
  <button class="post-deck__fs" type="button" onclick="var f=document.querySelector('.post-deck__frame'); if(f.requestFullscreen){f.requestFullscreen();}else{window.open('slides/deck.html','_blank');}">&#9974; Fullscreen</button>
</div>
