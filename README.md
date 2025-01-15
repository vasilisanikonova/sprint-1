# Спринт 1. 
## Часть 1.

После проведения анализа предложенного приложения, мною были сделаны основные выводы, которые позлужат отправными точками для дальнейшей декомпозици и предложения архитектуры:
1. Приложение, на данный момент, не большое, скорее всего предполагается задействование одной единой команды;
2. Приложение базируется на общем фреймворке - React.
В таком случае для реализации микрофронтендов мною выбран Webpack Module Federation, опираясь на п.2 выводов, а также использование Webpack Module Federation позволит наиболее эффективно осуществить вертикальную декомпозицию приложения на микрофронтенды.

Опираясь на принципы DDD (Domain-Driven Design) мною выделены следующие микрофронтенды:

1. auth-mcr — микрофронтенд, содержащий компоненты для регистрации и авторизации пользователей.
2. profile-mcr - микрофронтенд, содержащий компоненты профиля пользователя.
3. gallery-mcr — микрофронтенд, для хранения, отображения, управления фотографиями и "likes".
4. common-mcr — микрофронтенд, содержащий общие компоненты.


Ниже приведена предлагаемая структура предложения (в части фронтенда): 

 **auth-mcr** - Аутентификация

frontend/microfrontend/auth-mcr/
├── components/
│ ├── InfoTooltip.js # Компонент для отображения статуса сообщения о регистрации
│ ├── Login.js # Форма логина
│ ├── Register.js # Форма регистрации
│ └── ProtectedRoute.js # Роутер для маршрута авторизации
├── utils/
│ └── auth.js # API aутентификации и управление токенами
├── webpack.config.js
├── blocks/
│ │── auth-form/ # Стили для авторизации
│ │ ├── auth-form.css
│ │ ├── __button/
│ │ ├── __form/
│ │ ├── __input/
│ │ ├── __link/
│ │ ├── __text/
│ │ ├── __textfield/
│ │ ├── __title/
│ │ └── auth-form.css
│ └── login/
│ └── login.css 
├── contexts/
│ └── CurrentUserContext.js # user context для авторизации
├── index.js # Точка входа
├── index.css # Основные стили
└── package.json # Зависимости


**profile-mcr** - Профиль пользователя


frontend/microfrontend/profile-mcr/
├── components/
│ ├── EditAvatarPopup.js # Popup обновления аватара
│ │── EditProfilePopup.js # Popup редактирования профиля
│ └── PopupWithForm.js # Базовый компонент для Popup
│── blocks/
│ └── profile/ # Стили для профиля
│ ├── profile.css
│ ├── __description/ 
│ ├── __title/ 
│ ├── __image/ 
│ ├── __info/ 
│ ├── __edit-button/ 
│ └── __add-button/
├── contexts/
│ └── CurrentUserContext.js #  user context для авторизации
│── utils/
│ └── api.js # API для работы с данными пользователя
├── index.js # Точка входа 
├── index.css # Основные стили
└── package.json # Зависимости 



**gallery-mcr** - Галлерея фотографий


frontend/microfrontend/gallery-mcr/
├── components/
│ ├── Card.js # Компонент карточки с фото
│ ├── ImagePopup.js # Попап для просмотра фото
│ ├── AddPlacePopup.js # Попап добавления новой карточки
│ └── PopupWithForm.js # Базовый компонент для попапов
├── blocks/
│ ├── card/ # Стили для карточки
│ │ ├── card.css
│ │ ├── __description/
│ │ ├── __image/
│ │ ├── __title/
│ │ ├── __like-button/
│ │ │ └── _is-active/
│ │ ├── __like-count/
│ │ └── __delete-button/
│ │ ├── _hidden/
│ │ └── _visible/
│ ├── places/ # Стили для галереи карточек
│ │ ├── places.css
│ │ ├── __list/
│ │ └── __item/
│ └── popup/ # Стили для попапов
│ │ ├── popup.css
│ │ ├── __content/
│ │ ├── __close/
│ │ ├── __error/
│ │ ├── __icon/
│ │ ├── __label/
│ │ ├── __status-message/
│ │ ├── __title/
│ │ ├── __form/
│ │ ├── __input/
│ │ ├── __button/
│ │ ├── __caption/
│ │ ├── __image/
│ │ ├── __type/
│ │ └── _is-opened/
├── contexts/
│ └── CurrentUserContext.js # user context для авторизации
├── utils/
│ └── api.js # API для работы с карточками
├── index.js # Точка входа
├── index.css # Основные стили
└── package.json # Зависимости


**common-mcr** - Галлерея фотографий
frontend/microfrontend/host/
├── components/
│ ├── Header.js # Хэдер с навигацией
│ ├── Footer.js # Футер
│ ├── Main.js # Основной контейнер
├── blocks/
│ ├── header/ # стили Хэдера
│ │ ├── header.css
│ │ ├── __logo/
│ │ ├── __auth-link/
│ │ ├── __wrapper/
│ │ ├── __user/
│ │ └── __logout/
│ ├── footer/ # Стили футера
│ │ ├── footer.css
│ │ └── __copyright/
│ ├── page/ # Стили страницы
│ │ ├── page.css
│ │ ├── __content/
│ │ └── __section/
│ └── content/ # Стили контента
│ └── content.css
├── contexts/
│ └── CurrentUserContext.js # user context для авторизации
├── utils/
│ └── api.js # API 
├── index.js # Точка входа
├── index.css # Основные стили
├── logo.svg 
├── serviceWorker.js 
│ └── setupTests.js 
├── public/
│ └── index.html # HTML шаблон
│ └── favicon.ico
│ └── logo192.png
│ └── logo512.png
│ └── manifest.json
│ └── robots.txt
└── package.json # Зависимости

## Часть 2.
Ссылка на решенное 2 задание. Открыт доступ для комментирования
https://drive.google.com/file/d/168TedcvaX4axxmI0kY9sC9Ikg9J8VIfi/view?usp=sharing