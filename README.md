# Virtual machine
![digital ocean](https://github.com/ykropchik/web_starterPack/blob/main/Digital%20ocean.png)

# Request and Response 
1. vk.com/feed
  Не понял как определяется, что пользователь уже авторизован и можно грузить контент, но подозреваю, что это благодаря куче непонятных куки.

2. youtube.com
  Первое что бросилось в глаза такой кусок запроса
```
x-client-data: CIm2yQEIpLbJAQjEtskBCKmdygEIq7jKAQj1x8oBCOfIygEI6cjKAQi0y8oBCN3OygEIwdfKAQif2MoB
Decoded:
message ClientVariations {
  // Active client experiment variation IDs.
  repeated int32 variation_id = [3300105, 3300132, 3300164, 3313321, 3316779, 3318773, 3318887, 3318889, 3319220, 3319645, 3320769, 3320863];
}
```
Выглядит так, будто отправляется захешированный id пользователя, а в дагонку как бы возможные варианты расшифровки хеша. В остальном как обычно, куча непонятных куки.

3. translate.google.ru
  Точно также как у youtube 
```
x-client-data: CIm2yQEIpLbJAQjEtskBCKmdygEIq7jKAQj1x8oBCOfIygEI6cjKAQi0y8oBCN3OygEIwdfKAQif2MoB
Decoded:
message ClientVariations {
  // Active client experiment variation IDs.
  repeated int32 variation_id = [3300105, 3300132, 3300164, 3313321, 3316779, 3318773, 3318887, 3318889, 3319220, 3319645, 3320769, 3320863];
}
```
Видимо это фишка гугла.

4. github.com
  Аналогично, ничего интересного не наблюдается, запрос абсолютно дефолтный, куки, какие-то поля, отличаются только значения в этих полях. Ответы тоже не особо отличаются, только в значениях, но структура шаблонная

5. dvfu.ru
  Даже здесь ничего необычного, хотя я очень этого ждал...

6. univer.dvfu.ru
  Единственное, что показалось интересным, это в куки строчка ``` expires=Sun, 08-Nov-2020 07:01:43 GMT; ```, думаю это время когда истечет сеанс авторизации на этом устройстве, но это не точно.
  
7. Дальше чекнул еще instagram.com, web.telegram.org и yandex.ru  Но аналогично, ничего интересного не нашел

# Autorization 
1. vk.com 
  В запросе отправляется логин и пароль, даже не шифруется, а в ответ приходит видимо одобрение на правильность данных
2. instagram.com 
  Уже интереснее, потому что тут из-за дфухфакторной аутентификации клиент отправляетс запрос на авторизацию с логином и паролем, в ответе говорится о том, что необходимо пройти вторую аутентификацию и с этого момента клиент с определенным интервалом шлет запросы типа: "ну чо там, авторизация прошла", в приходят коды на отказ и когда приходит подтверждение, происходит открузка страницы.

# Communication 
![digital ocean](https://github.com/ykropchik/web_starterPack/blob/main/Tellnet.png)
