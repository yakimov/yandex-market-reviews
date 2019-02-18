# yandex-market-reviews
Замена публичному Yandex.API. Получение ТОП10 отзывов и информации о магазине.

## Пример использования
```PHP
<?php

require 'vendor/autoload.php';

use S25\Scrapping\Reviews;

// Скачиваем страницу с отзывами
$html   = new HTTPClient();
$result = $html->get('https://market.yandex.ru/shop--ozon-ru/443605/reviews');

$review  = new Reviews($result);

// 10 последних отзывов со страницы магазина
$reviews = $review->getLastTenReviews();

// Кол-во оценок для 5,4,3,2,1 звёзд
$stars   = $review->getStars();

// Прочая информация со страницы отзывов
$summary = $review->getSummaryRating();

?>
```

### 10 последних отзывов со страницы магазина

```PHP
$reviews = $review->getLastTenReviews();
var_dump($reviews);

‌array (
  0 => 
  array (
    'id' => '87359237',
    'date' => '2019-02-17',
    '‌‌author' => 'Владислав',
    'ratingValue' => '4',
    'img' => '//avatars.mds.yandex.net/get-yapic/54535/41833720-1557781046/islands-retina-middle',
    'delivery' => 'самовывоз',
    'city' => 'Болохово',
    'review' => 
    array (
      'positive' => 'Переодически бывают хорошие скидки на товары которых осталось мало. ',
      'negative' => 'Платная доставка до пункта самовывоза невелирует те скидки которые бывают в этом магазине. ',
      'comment' => 'Очень люблю и рекомендую. Новая политика порадовала. Купила подписку и продолжаю радоваться удобству, сервису, ассортименту. Благодарю вас за ваш труд!',
    ),
  ),
more 9...
}
```

### Кол-во оценок для 5,4,3,2,1 звёзд

```PHP
$stars   = $review->getStars();
var_dump($stars);

‌array (
  5 => 
  array (
    'value' => '50',
    'count' => '6289',
  ),
  4 => 
  array (
    'value' => '12',
    'count' => '1505',
  ),
  3 => 
  array (
    'value' => '12',
    'count' => '1533',
  ),
  2 => 
  array (
    'value' => '6',
    'count' => '776',
  ),
  1 => 
  array (
    'value' => '19',
    'count' => '2374',
  ),
)
```

### Прочая информация со страницы отзывов
```PHP
$summary = $review->getSummaryRating();
var_dump($summary);

‌array (
  'Удобство самовывоза' => '4,6',
  'Скорость и качество доставки' => '4,2',
  'Скорость обработки заказа' => '4,6',
  'Общение' => '4,4',
  'Соответствие товара описанию' => '4,6',
  'рейтинг за 3 месяца' => '43',
  'за 3 месяца' => '4043',
  'за всё время' => '63847',
  '% покупателей купили бы здесь снова' => '87',
)
```