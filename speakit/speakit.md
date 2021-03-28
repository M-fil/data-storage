# SpeakIt

**SpeakIt** - одностраничное приложение, при помощи которого можно прослушать произношение английских слов и использовать технологию распознавания речи Google Web Speech API для проверки правильности произношения.

## Демо приложения:
**Demo** https://speakit.netlify.com/ (версия без Hacker scope)

## Исходные данные

Коллекция из 3600 часто употребляемых английских слов, отсортированных в порядке возрастания сложности. Вся коллекция разбита на шесть частей по 600 слов в каждой. Для каждого слова предлагается транскрипция, пример произношения, картинка-ассоциация. Есть и другие данные, но они в этом таске не используются. Переводов слов в исходных данных нет, их нужно будет получить при помощи translation API. 

## Работа приложения
- При первом заходе в приложение должна быть форма авторизации и регистрации (логин и пароль). После аутентификации пользователья должно редиректить на страницу с большой кнопкой START.
- После перезагрузки страницы авторизированный пользователь должен быть переведен на страницу с большой кнопкой START
- После нажатия на кнопку START отображаются слова.
- На главной странице со словами должен отображаться логин пользователя
- Должна быть возможность выйти из своего аккаунта.
- Должна быть страница со статистикой. Статистика должна сохранятся для всех пользователей. На странице статистики должна быть таблица со следующими данными: имя пользователя, количество правильных и неправильных ответов, группа слов (всех 6 групп) и дата игры.
- Сортировка в статистике должна быть по баллам за игру и по группе слов. 1-я группа слов - самая легкая, 6-я - самая сложная. Соответственно, если будет пользователь, у котого 8 правильных ответов и 2 неправильных с группой слов 6, а у другого 10 правильных и 0 неправильных и группа 1, то 1-й пользователь должен быть на 1-м месте. Для простоты сортировки можно сделать следующий множитель для количества баллов: Х1 - для 1-го уровная, Х1.1 - для 2-го, ... , Х1.5 - для 6-го. То есть если с 6-й группой слов набрано 5 правильных ответов, то это будет 5 * 1.5 = 7.5
- слова выводятся на страницу группами по 10 слов. Возле каждого слова отображается транскрипция и иконка аудио  
- при клике по слову звучит его произношение, выводятся соответствующие данному слову картинка и перевод 
- у пользователя есть возможность включить (и отключить) распознавание речи Google Speech Recognition
- если распознавание речи включено, и приложению разрешён доступ к микрофону, все произнесённые пользователем слова распознаются и отображаются в текстовом виде
- проверка правильности произношения происходит путём сравнения распознанного текста с написанием слова
- приложение сохраняет результаты тренировки произношения каждой группы слов и позволяет их просматривать

## Требования к репозиторию
- демо-версия приложения размещается на heroku: https://www.heroku.com/
- **ВАЖНО!** Для работы над проектом нужно использовать GitHub M-fil. Логин и пароль будет выдан. Когда проект будет склонирован, то нужно обязательно проверить, что указано в git для email и name. Для этого есть специальные команды: git config user.name и git config user.email. Данные команды должны выводить "Maxim Filanovich" и "filanovich.maxim11b@mail.ru". Если будут указаны не эти данные, то в коммитах и GitHub репозитории будет отмечен не правильный автор.

## Технические требования
- работа приложения проверяется в браузере Google Chrome последней версии
- Для разработки нужно использовать библиотеку React
- Для авторизации, регистрации и сохранения результатов в БД нужно использовать Firebase
- Нужно использовать Redux
- Должен быть подключен ESLINT
- Обязательно требование: использование TypeScript.
- Структура папок приложения должны быть как в этом примере: https://github.com/M-fil/react-chat-app/tree/master/client

## Ключевые навыки

- получение данных о словах (предлагаемый набор слов является частью данных, которые будут использованы для финального проекта)
- работа с асинхронными запросами
- использование translation API
- использование Google Web Speech API 
- Работа с технологими Redux, React, Redux Saga
- Использование Firebase в качестве бэкенда

## Видео с разбором задания
https://youtu.be/k7kKaa5KwBs

## Информационные ресурсы
- Использование распознавания речи для тренировки произношения https://youtu.be/XbjGZHeLUn8  

## Материалы
- Вебинар: Асинхронность в JavaScript https://youtu.be/Ih6Q7ka2eSQ
- Yandex.Translate API https://tech.yandex.com/translate/
- Web API SpeechRecognition https://developer.mozilla.org/ru/docs/Web/API/SpeechRecognition
- JavaScript Speech Recognition https://youtu.be/0mJC0A72Fnw
- Визуализация исходных данных https://rslang-data.netlify.com/

## Пример использования Yandex Translate API
- Получаем Yandex.Translate API key  
`https://translate.yandex.com/developers/keys`
- Перевод слова "agree"  
`https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20200322T155651Z.de98a60e6a99185e.089aea4237b51c6db082c966f27a7895cd1e8b44&text=agree&lang=en-ru`

<details> 
  <summary>Примеры асинхронных запросов</summary>

  <p></p>

  JS-код для получения перевода слова (перевод выводится в консоль)

  - при помощи fetch
   ``` javascript 
   function getTranslation () {
   const url = 'https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20200322T155651Z.de98a60e6a99185e.089aea4237b51c6db082c966f27a7895cd1e8b44&text= agree &lang=en-ru';
   fetch(url)
     .then(res => res.json())
     .then(data => {
       console.log(data.text)
     });
   }
  ```
  
  - при помощи async/await
  
  ``` javascript 
   async function getTranslation () {
     const url = 'https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20200322T155651Z.de98a60e6a99185e.089aea4237b51c6db082c966f27a7895cd1e8b44&text= agree &lang=en-ru';
     const res = await fetch(url);
     const data = await res.json();
     console.log(data.text);
   }
  ```

</details> 

### Документ для вопросов
- документ для вопросов, связанных с выполнением задания: https://docs.google.com/spreadsheets/d/1owDtS2YLnF9ijSNjPtcPmpiFql8jcfQ6d4OB6zz53zE/edit#gid=0
- ссылки на лучшие работы добавьте, пожалуйста, в эту форму: https://forms.gle/xo514226dk3VWaZ47

## Пример получения данных по словам при помощи Fetch API

Для этого создан REST API по адресу: `https://afternoon-falls-25894.herokuapp.com/`  
На данный момент можно пользоваться следующим GET эндпоинтом для получения списка слов:  
`https://afternoon-falls-25894.herokuapp.com/words?page=2&group=0` - получить слова со 2-й страницы группы 0  
Строка запроса должна содержать в себе номер группы и номер страницы. Всего 6 групп(от 0 до 5) и в каждой группе по 30 страниц(от 0 до 29). В каждой странице по 20 слов. Группы разбиты по сложности от самой простой(0) до самой сложной(5).  

REST сервис возвращает только JSON, без изображений и звуковых файлов. 

<details> 
  <summary>Примеры асинхронных запросов</summary>

  <p></p>

  JS-код для получения списка слова (слова выводятся в консоль)

  - при помощи fetch
  
   ``` javascript 
    const getWords = async (page, group) => {
        const url = `https://afternoon-falls-25894.herokuapp.com/words?page=${page}&group=${group}`;
        const res = await fetch(url);
        const json = await res.json();
        console.log(JSON.stringify(json, null, 1));
    };  
  ```
  
   - пример результат вызова
   
 ```json
    [
     {
      "word": "camera",
      "image": "files/01_0007.jpg",
      "audio": "files/01_0007.mp3",
      "audioMeaning": "files/01_0007_meaning.mp3",
      "audioExample": "files/01_0007_example.mp3",
      "textMeaning": "A <i>camera</i> is a piece of equipment that takes pictures.",
      "textExample": "I brought my <b>camera</b> on my vacation.",
      "transcription": "[kǽmərə]",
     },
     {
      "word": "capital",
      "image": "files/01_0008.jpg",
      "audio": "files/01_0008.mp3",
      "audioMeaning": "files/01_0008_meaning.mp3",
      "audioExample": "files/01_0008_example.mp3",
      "textMeaning": "A <i>capital</i> is a city where a country’s government is based.",
      "textExample": "The <b>capital</b> of the United States is Washington, D.C.",
      "transcription": "[kæpətl]",
     },
     {
      "_id": "5e8aaaf87c3d1d199c0f2d76",
      "word": "catch",
      "image": "files/01_0009.jpg",
      "audio": "files/01_0009.mp3",
      "audioMeaning": "files/01_0009_meaning.mp3",
      "audioExample": "files/01_0009_example.mp3",
      "textMeaning": "To <i>catch</i> is to grab or get something.",
      "textExample": "Did you <b>catch</b> the ball during the baseball game?",
      "transcription": "[kætʃ]",
     }
     
     ...
     
    ]
```
Для получения изображений и звуков можно форкнуть репозиторий по ссылке: `https://github.com/irinainina/rslang-data`  
После получения списка слов можно будет создавать новые HTML элементы с ссылками на нужные файлы.  
Например, для изображение `files/01_0009.jpg` надо создать следующий элемент:  
`<img src="https://raw.githubusercontent.com/YOUR-GITHUB-USERNAME/rslang-data/master/data/01_0009.jpg">`  
обратите внимание, что вместо YOUR-GITHUB-USERNAME надо подставить свои данные. Так же, то что в ссылку подставляется  только имя файла без директории `file/`
</details> 
