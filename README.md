# Hides-annoying-YouTube-stream-recordings.

Для работы надо скачать [Violentmonkey](https://github.com/violentmonkey/violentmonkey) или [Tampermonkey](https://github.com/Tampermonkey/tampermonkey)

Можно просто перейти на [GresyFork](https://greasyfork.org/ru) и нажать на [установить](chrome-extension://jinjaccalgkegednnccohejagnlnfdag/confirm/index.html#VMr8p29gmrm1m) или же скопировать код ниже

```
// ==UserScript==
// @name         Скрыть записи трансляций на YouTube
// @namespace    Violentmonkey Scripts
// @version      1.0
// @description  Скрывает записи трансляций на YouTube (с подписью "Трансляция закончилась ... назад").
// @author       KryptonFG
// @match        https://www.youtube.com/*
// @grant        none
// ==/UserScript==
 
(function () {
  'use strict';
 
  const observer = new MutationObserver(hideEndedStreams);
  const targetNode = document.body;
  const config = { childList: true, subtree: true };
 
  // Шаблон "Трансляция закончилась ... назад" — с разными единицами времени
  const endedStreamRegex = /Трансляция закончилась\s.+назад/i;
 
  function hideEndedStreams() {
    const items = document.querySelectorAll('ytd-video-renderer, ytd-grid-video-renderer, ytd-rich-item-renderer');
 
    items.forEach(item => {
      if (item.innerText.match(endedStreamRegex)) {
        item.style.display = 'none';
      }
    });
  }
 
  // Запустить сразу и потом следить за изменениями
  hideEndedStreams();
  observer.observe(targetNode, config);
})();
```
