<h1> Инструкция </h1>
<h2> 1. Создание структуры проекта </h2>

<ol>
  <li>
    <strong>mkdocs.yml</strong> — конфигурационный файл для генератора документации MkDocs. Здесь задаются название сайта, тема, навигация и плагины.
  </li>
  <li>
    <strong>docs/</strong> — папка, содержащая все страницы сайта в формате Markdown (.md). Это источник контента для генерации.
  </li>
  <li>
    <strong>docs/index.md</strong> — главная страница сайта. Именно она открывается при заходе на сайт.
  </li>
  <li>
    <strong>.github/workflows/deploy.yml</strong> — файл конфигурации GitHub Actions, автоматизирующий процесс сборки и деплоя сайта на GitHub Pages.
  </li>
</ol>

<h2>2) Локальная сборка и запуск сайта через Docker</h2>
<p>Для предварительного просмотра сайта на локальной машине используем Docker:</p>

<pre><code>docker run --rm -it -p 8000:8000 -v $(pwd):/docs squidfunk/mkdocs-material serve</code></pre>

<p>После запуска откройте <a href="http://localhost:8000" target="_blank">http://localhost:8000</a> в браузере.</p>

<h2>3) Сборка сайта для деплоя</h2>
<p>Для генерации статических файлов сайта выполните:</p>

<pre><code>docker run --rm -v $(pwd):/docs squidfunk/mkdocs-material build</code></pre>

<p>Сайт будет собран в папке <code>site/</code>.</p>

<h2>4) Автоматизация деплоя через GitHub Actions</h2>

<p>Для автоматической публикации сайта на GitHub Pages необходимо:</p>

<ul>
  <li>Создать файл <code>.github/workflows/deploy.yml</code> с конфигурацией GitHub Actions.</li>
  <li>Добавить в настройки репозитория секретный токен <strong>GH_PAT</strong> с правами на пуш в ветку <code>gh-pages</code>.</li>
</ul>

<h3>Как добавить токен GH_PAT</h3>

<ol>
  <li>Перейдите в настройки вашего репозитория:<br>
      <em>Settings -> Secrets and variables -> Actions -> New repository secret</em>
  </li>
  <li>Назовите секрет <code>GH_PAT</code>.</li>
  <li>Создайте <a href="https://github.com/settings/tokens" target="_blank">Personal Access Token</a> с правами:
    <ul>
      <li><code>repo</code></li>
      <li><code>workflow</code></li>
    </ul>
  </li>
  <li>Вставьте токен в поле значения и сохраните.</li>
</ol>

<h3>Публикация изменений</h3>

<p>После настройки проекта и добавления workflow необходимо закоммитить и отправить изменения в репозиторий:</p>

<pre><code>git add .
git commit -m "deploy"
git push origin main
</code></pre>

<p>После этого GitHub Actions автоматически запустит сборку и деплой.</p>

<h3>Настройка GitHub Pages</h3>

<ol>
  <li>Перейдите в <em>Settings -> Pages</em> вашего репозитория.</li>
  <li>В разделе <em>Source</em> выберите ветку <code>gh-pages</code> и директорию <code>/ (root)</code>.</li>
  <li>Сохраните настройки. Через несколько секунд сайт будет доступен по указанной ссылке.</li>
</ol>
