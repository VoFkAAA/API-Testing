# Требования

#### Логика выбора курьерской службы при оформлении заказа пользователем: 

* должна работать в указанное в заказе время 
* должна быть самой дешёвой.

Пользователю отображается время доставки в зависимости от выбранной службы.

В заказе доставка становится платной, если соблюдается хотя бы одно условие:

* превышено максимальное количество товаров;
* превышен максимальный вес;
* сумма заказа меньше 150 рублей.

#### Логика расчёта стоимости доставки заказа для пользователя:

- Если вес или количество превысили максимальное значение, стоимость доставки для пользователя становится 99 рублей.
- Если вес или количество в заказе не превышают максимального, берётся `price` этих продуктов, и если их сумма меньше 150 рублей, то стоимость доставки для пользователя также становится 99 рублей.

Стоимость доставки прибавляется в итоговую сумму заказа.

Если ни одно из обозначенных условий не соблюдается, то цена доставки курьерской службы не включается в итоговую сумму заказа.

Цена доставки курьерской службой рассчитывается по количеству и весу указанных продуктов.

Вычисление зависит от передаваемых переменных `productsCount` (количество продуктов) и `productsWeight` (вес продуктов).


Например, для службы доставки «Доставка Москва»:

`` ЕСЛИ `productsCount` меньше или равно `10 шт.` ``

`` И `productsWeight` меньше или равно `3 кг` ``

`` ТО `hostDeliveryCost` будет равен `25` ``

 

Во всех остальных случаях `hostDeliveryCost` будет равен `45` .

 

- `clientDeliveryCost` — стоимость доставки клиенту рассчитывается в соответствии с таблицей.

<table style="border-collapse: collapse; width: 100%; text-align: center;">
  <tr style="background: #f0f0f0;">
    <th style="border: 1px solid black; padding: 8px; text-align: center;">Наименование доставки</th>
    <th style="border: 1px solid black; padding: 8px; text-align: center;">Время работы</th>
    <th style="border: 1px solid black; padding: 8px; text-align: center;">Количество товаров в заказе, шт</th>
    <th style="border: 1px solid black; padding: 8px; text-align: center;">Вес заказа</th>
    <th style="border: 1px solid black; padding: 8px; text-align: center;">Время доставки</th>
    <th style="border: 1px solid black; padding: 8px; text-align: center;">Цена доставки курьерской службы, руб.</th>
    <th style="border: 1px solid black; padding: 8px; text-align: center;">Формат данных</th>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">Доставка Москва</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">08-22</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">0-10</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">0-3 кг</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">30-35 мин</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">25</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">JSON</td>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">Доставка Москва</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">08-22</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">11-15</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">3,1-7 кг</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">30-35 мин</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">45</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">JSON</td>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">Привезём быстро</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">07-21</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">0-7</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">0-2,5 кг</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">25-30 мин</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">23</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">XML</td>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">Привезём быстро</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">07-21</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">8-14</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">2,6-6 кг</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">25-30 мин</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">43</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">XML</td>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">Чух-чух и уже у вас</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">06-20</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">0-12</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">0-3,5 кг</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">25-30 мин</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">29</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">XML</td>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">Чух-чух и уже у вас</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">06-20</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">13-20</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">3,6-9 кг</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">25-30 мин</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">53</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">XML</td>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">На метле уюта</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">08-22</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">0-9</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">0-3 кг</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">20-25 мин</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">25</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">JSON</td>
  </tr>
  <tr>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">На метле уюта</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">08-22</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">13-20</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">3,1-6 кг</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">20-25 мин</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">40</td>
    <td style="border: 1px solid black; padding: 8px; text-align: center;">JSON</td>
  </tr>
</table>


Вычисление зависит от передаваемых переменных `productsCount` (количество продуктов) и `productsWeight` (вес продуктов).

  Стоимость доставки клиенту может быть равна 0 и 99.

  Стоимость доставки будет 99, если соблюдается хотя бы одно из условий:
  - превышено максимальное количество товаров;
  - превышен максимальный вес.

 

Например, для службы доставки «Доставка Москва»:

`` ЕСЛИ `productsWeight` больше `7 кг` (максимальное значение по таблице) ``

`` ИЛИ `productsCount` больше `15 шт.` (максимальное значение по таблице) `` 

`` ТО `clientDeliveryCost` будет равна `99` ``

 

Во всех остальных случаях `clientDeliveryCost`  будет равен `0` .
