# Rovos-HTTP брокер.

Представляет из себя объеиненный TCP и HTTP сревер. Предоствляет REST протокол
для общения с вендинговым аппаратом.

# Запуск сервера

> bundle exec rackup

# Команды (ответ в JSON)

## Сколько и какие машины в подключении

> curl http://localhost:8080/machines/

## Получить статус машины (время последней активности)

> curl http://localhost:8080/machines/:id

Например:

> curl http://localhost:8080/machines/100020003

## Изменить режим (состояние) работы машины

> curl -XPOST http://localhost:8080/machines/100020003?state=СОСТОЯНИЕ&work_time=ВРЕМЯ________В___МИНУТАХ

Например включить машину в режим "Стандартный массаж" на 2 минуты:

> curl -XPOST http://localhost:8080/machines/100020003?state=2&work_time=4

## Режимы работы машины

* 0 - Аппарат загружается
* 1 - Кресло в режиме ожидания команды
* 2 - Стандартный массаж (на указанное количество времени)
* 3 - Не известный
* 4 - Запрос состояния вендинговой машины
* 5 - Разбудить тело (зарезервированная функция)
* 6 - Передача Ци и Крови (зарезервированная функция)
* 7 - Диастола (зарезервированная функция)
* 8 - Массаж талии (зарезервированная функция)
* 9 - Массаж шеи (зарезервированная функция)
* 255 - Сброс (в режиме сброса). Сбрасывает оставшееся время (`elapsed_time`)
  если оно было закинуто в 65536. Не влияет на уже запущенную машину.

## Rovos: Тарифы

* 5 минут 50 руб
* 10 мин 90 руб
* 20 мин 150 руб

## TODO

* https://www.codebasehq.com/blog/ruby-threads-queue
