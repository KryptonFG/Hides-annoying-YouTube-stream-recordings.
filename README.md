# Hides-annoying-YouTube-stream-recordings.

Для работы надо скачать [Violentmonkey](https://github.com/violentmonkey/violentmonkey) или [Tampermonkey](https://github.com/Tampermonkey/tampermonkey)

Можно просто перейти на [GresyFork]([https://greasyfork.org/ru](https://greasyfork.org/ru/scripts/540383-%D1%81%D0%BA%D1%80%D1%8B%D1%82%D1%8C-%D0%B7%D0%B0%D0%BF%D0%B8%D1%81%D0%B8-%D1%82%D1%80%D0%B0%D0%BD%D1%81%D0%BB%D1%8F%D1%86%D0%B8%D0%B9-%D0%BD%D0%B0-youtube/code)) и нажать на [установить](chrome-extension://jinjaccalgkegednnccohejagnlnfdag/confirm/index.html#VMr8p29gmrm1m) или же скопировать код ниже

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
