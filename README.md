# Написать symfony приложение для рассчета цены продукта и проведение оплаты (REST)

## Исходные данные:
HTTP POST запрос с JSON body.

### Пример запроса:
```
{
    "productType" : "digital",
    "product": "UNIQUE_ID1",
    "taxNumber": "DE123456789",
    "paymentProcessor": "paypal"
}
```

```
{
    "productType" : "physical",
    "product": "UNIQUE_ID2",
    "taxNumber": "GR123456789",
    "paymentProcessor": "stripe"
}
```

## Выходные данные:

1. Если оплата прошла удачно, то HTTP ответ с кодом 200
2. Если не прошла валидация или не прошла оплата, то HTTP ответ с кодом 400 и JSON с валидационными ошибками

## Продукты:
### Продавец продает два физических продукта

- телефон Samsung (100 евро), налог 20%
- чехол для телефона (20 евро), налог 10%

### и два курса (digital):

- курс "Первый курс" (10 евро)
- курс "Второй курс" (15 евро)


## Расчет налога:
### Налог на физические товары (physical) постоянный для определенного продукта и не изменяется относительно страны покупателя.
Для покупателя телефон Samsung из Греции цена составляет 120 евро (цена продукта 100 + налог 20%).

### При покупке цифрого продукта (digital) получатель сверх цены продукта должен уплатить налог, относительно страны налогового номера:
- Германии - 19%
- Италии - 22%
- Греции - 24%

В итоге для покупателя курса "Первый курс" из Греции цена составляет 12,4 евро (цена продукта (10 евро + налог 24%).

## Формат налогого номера:
DEXXXXXXXXX - для жителей Германии
ITXXXXXXXXXXX - для жителей Италии
GRXXXXXXXXX - для жителей Греции,
где первые два символа - это код страны, а X - это любая цифра от 0 до 9

## Задача:
После отправки формы, нужно проверить корректность tax номера, расчитать итоговую цену покупки вместе с налогом, провесети оплату, вызвав PaypalPaymentProcessor::pay или StripePaymentProcessor::processPayment (прилагаются, их нужно скопировать себе в проект тестового задания).

Необходимо использовать компонент Symfony Form, Validator.
При написании тестового используйте git, после выполнения пришлите ссылку на репозиторий.

## Желательно:
- приложить Dockerfile (docker compose)
- PHP Unit test
- применение SOLID принципов
