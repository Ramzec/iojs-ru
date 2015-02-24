# Таймеры

    Стабильность: 5 - Заблокирован ????

Все функции для управления таймерами являются глобальными.
Вам не нужно делать require() какого либо модуля для получения
доступа к данным функциям.

## setTimeout(callback, delay[, arg][, ...])

Однократный вызов функции обратного вызова по истечению `delay` миллисекунд.
Возвращает объект `timeoutObject`, который может использоваться для остановки
таймера при помощи `clearTimeout()`. По необходимости можно указать аргументы,
которые будут переданы в функцию обратного вызова.

Важно помнить что функция обратного вызова вероятно не будет вызвана в точности
после `delay` миллисекунд - io.js не дает гарантий как в точности отсчета времени,
по истечении которого будет вызвана функция обратного вызова, так и в порядке их
вызова. Функция обратного вызова будет вызвана настолько близко к указанному значению
насколько это будет возможно.

## clearTimeout(timeoutObject)

Останавливает однократный таймер, на который указывает `timeoutObject`

## setInterval(callback, delay[, arg][, ...])

Периодический вызов функции обратного вызова каждый `delay` миллисекунд.
Возвращает объект `intervalObject`, который может использоваться для остановки
таймера при помощи `clearInterval()`. По необходимости можно указать аргументы,
которые будут переданы в функцию обратного вызова.

## clearInterval(intervalObject)

Останавливает интервальный таймер, на который указывает `intervalObject`. 

## unref()

The opaque value returned by `setTimeout` and `setInterval` also has the method
`timer.unref()` which will allow you to create a timer that is active but if
it is the only item left in the event loop won't keep the program running.
If the timer is already `unref`d calling `unref` again will have no effect.

In the case of `setTimeout` when you `unref` you create a separate timer that
will wakeup the event loop, creating too many of these may adversely effect
event loop performance -- use wisely.

## ref()

If you had previously `unref()`d a timer you can call `ref()` to explicitly
request the timer hold the program open. If the timer is already `ref`d calling
`ref` again will have no effect.

## setImmediate(callback[, arg][, ...])

Немедленный вызов `callback` после вызова всех функций обратного вызова,
которые ожидают событий от подсистемы ввода-вывода, но перед функциями,
который запланированы при помощи `setTimeout` и `setInterval`. Возвращает
объект `immediateObject`, который может использоваться для остановки таймера
при помощи `clearImmediate()`. По необходимости можно указать аргументы,
которые будут переданы в функцию обратного вызова.

Функции обратного вызова в данном случае ставятся в очередь в порядке создания
объектов `immediateObject`. Данная очередь обрабатывает на каждой итерации цикла.
Если Вы создали `immediateObject` внутри какой либо функции обратного вызова, тогда
запланированная функция не будет вызвана до следующей итерации цикла.

## clearImmediate(immediateObject)

Останавливает таймер немедленного вызова, на который указывает объект `immediateObject`
