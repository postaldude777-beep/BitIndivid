const CACHE_NAME = 'recipe-app-v1';
const PRECACHE_URLS = ['./index.html', './manifest.json'];

// Установка: сохраняем основные файлы в кэш
self.addEventListener('install', (event) => {
  event.waitUntil(
    caches.open(CACHE_NAME).then((cache) => cache.addAll(PRECACHE_URLS))
  );
  self.skipWaiting();
});

// Обработка запросов: сначала ищем в кэше, если нет - грузим из сети
self.addEventListener('fetch', (event) => {
  event.respondWith(
    caches.match(event.request).then((response) => {
      return response || fetch(event.request);
    })
  );
});