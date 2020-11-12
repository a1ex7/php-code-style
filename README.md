Цель данных рекомендаций — снижение сложности восприятия, поддержки, тестирования и расширения кода, написанного разными
авторами; она достигается путём рассмотрения серии правил и ожиданий относительно написания PHP-кода.

Слова «НЕОБХОДИМО» / «ДОЛЖНО» («MUST»), «НЕДОПУСТИМО» («MUST NOT»), «ТРЕБУЕТСЯ» («REQUIRED»), «НУЖНО» («SHALL»),
«НЕ ПОЗВОЛЯЕТСЯ» («SHALL NOT»), «СЛЕДУЕТ» («SHOULD»), «НЕ СЛЕДУЕТ» («SHOULD NOT»), «РЕКОМЕНДУЕТСЯ» («RECOMMENDED»),
«МОЖЕТ» / «ВОЗМОЖНО» («MAY») и «НЕОБЯЗАТЕЛЬНО» («OPTIONAL») в этом документе следует понимать так,
как это описано в [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt) (и его [переводе](http://rfc.com.ru/rfc2119.htm)).

## 1. Оформление

### 1.1. Базовый стандарт оформления кода

Код ДОЛЖЕН быть оформлен согласно всем правилам, указанным в стандарте [PSR-12](https://www.php-fig.org/psr/psr-12/).

### 1.2. Строки

Жесткое ограничение строки ДОЛЖНО составлять 120 символов.
В случае превышения этого ограничения автоматические системы проверки стиля ДОЛЖНЫ считать это ошибочной ситуацией,
для таких ситуаций НЕОБХОДИМО явно отключать проверку стиля с помощью аннотаций:

* `// @codingStandardsIgnoreStart`
* `// @codingStandardsIgnoreStop`

> Это требование дополняет [PSR-12 2.3. Lines](https://www.php-fig.org/psr/psr-12/#23-lines).

```php
// @codingStandardsIgnoreStart
use VendorWithVerlyLongName\ProjectrWithVerlyLongName\ServicesWithVerlyLongName\ServiceFolderWithVerlyLongName\ClassWithVerlyLongName;
// @codingStandardsIgnoreStop
```

### 1.3. Выравнивание присвоений переменных и элементов массива

Блок присвоений ДОЛЖЕН быть выровнен по самому длинному присвоению в блоке.
Если операция присвоения превышает максимальную длину строки НЕОБХОДИМО:

 * или начать новый блок с помощью пустой строки;
 * или выражение должно быть перенесено на новую строку с отступом в 4 пробела,
   при этом оператор присвоения ДОЛЖЕН остаться на той же строке, что и переменная.

```php
// Правильно
$varName      = 'varName';
$variableName = 'variableName';
```

```php
// Не правильно
$varName = 'varName';
$variableName = 'variableName';
```

```php
// Правильно
$varName                            = 'varName';
$secondVariableWithVeryLongNameHere =
    '123456790123456790123456790123456790123456790123456790123456790123456790123456790';
```

```php
// Не правильно
$varName                            = 'varName';
$secondVariableWithVeryLongNameHere
    = '123456790123456790123456790123456790123456790123456790123456790123456790123456790';
```

```php
// Правильно
$firstVariableWithVeryLongNameHere = 'varName';

$variableName = '123456790123456790123456790123456790123456790123456790123456790123456790123456790';
```

```php
// Правильно
[
    'elementName'     => 'elementName',
    'longNameElement' => 'longNameElement',
]
```

```php
// Не правильно
[
    'elementName' => 'elementName',
    'longNameElement' => 'longNameElement',
]
```

```php
// Правильно
[
    'elementName'                       => 'elementName',
    'secondElementWithVeryLongNameHere' =>
        '123456790123456790123456790123456790123456790123456790123456790123456790123456790',
]
```

```php
// Не правильно
[
    'elementName'                       => 'elementName',
    'secondElementWithVeryLongNameHere'
        => '123456790123456790123456790123456790123456790123456790123456790123456790123456790',
]
```

```php
// Правильно
[
    'firstElementWithVeryLongNameHere' => 'elementName',

    'elementName' => '123456790123456790123456790123456790123456790123456790123456790123456790123456790',
]
```

### 1.4. Массивы

При объявлении многострочного массива в конце последнего объявления ДОЛЖНА ставиться запятая,
для однострочного массива запятую ставить НЕДОПУСТИМО.

```php
// Правильно
[
    'firstElement'  => 'firstElement',
    'secondElement' => 'secondElement',
]
```

```php
// Не правильно
[
    'firstElement'  => 'firstElement',
    'secondElement' => 'secondElement'
]
```

```php
// Правильно
['firstElement' => 'firstElement', 'secondElement' => 'secondElement']
```

```php
// Не правильно
['firstElement' => 'firstElement', 'secondElement' => 'secondElement',]
```


### 1.5. Последовательность вызовов (Chaining)

Каждый элемент вызова для последовательностей, состоящих из трех и более элементов ДОЛЖЕН находиться на новой строке.
В случае превышения максимальной длины строки каждый элемент последовательности вызовов
ДОЛЖЕН находиться на новой строке.

```php
// Правильно
$this->firstMethod();
```

```php
// Не правильно
$this
    ->firstMethod();
```

```php
// Правильно
$this
    ->firstMethod()
    ->secondMethod();
```

```php
// Не правильно
$this->firstMethod()->secondMethod();
```

```php
// Не правильно
$this
    ->firstMethod()->secondMethod();
```

```php
// Правильно
$this
    ->firstMethod()
    ->thirdMethod(
        $firstArgument,
        $secondArgument,
        $thirdArgument,
        $fourthArgument,
        $fifthArgument,
        $sixArgument
    );
```

```php
// Не правильно
$this->firstMethod()->thirdMethod(
    $firstArgument,
    $secondArgument,
    $thirdArgument,
    $fourthArgument,
    $fifthArgument,
    $sixArgument
);
```


### 1.6. Выделение управляющих инструкций

Управляющие инструкции: `if`, `for`, `foreach`, `while`, `do-while`, `switch`, `break`, `continue`, `return`
ДОЛЖНЫ отделяться от кода того же уровня вложенности одной пустой строкой.

```php
// Правильно
$count = 5;

if ($count === 5) {
// ...
}

// ...
```

```php
// Не правильно
$count = 5; // Отсутствует перевод строки
if ($count === 5) {
// ...
}
$length = 12; // Отсутствует перевод строки
// ...
```

```php
// Правильно
{
    if ($count === 5) {
    // ...
    }
}
```

```php
// Не правильно
{

    // Лишняя пустая строка
    if ($count === 5) {
    // ...
    }
    // Лишняя пустая строка
}
```

## 2. Документирование

### 2.1. Базовый стандарт для оформления документации в коде

Код ДОЛЖЕН быть оформлен согласно правилам, указанным в стандарте
[PSR-19](https://github.com/php-fig/fig-standards/blob/master/proposed/phpdoc-tags.md).

### 2.2. Дублирование типов в docblock

Указание типов аргументов с помощью `@param` и `@return`, дублирующее сигнатуру метода НЕДОПУСТИМО, кроме случаев:

* Наличия комментария к параметрку, или результату.
* Аннотации используются сторонними средствами: psalm, phan, phpstan, и т.д.

```php
// Правильно
public function incrementProductPriceByName(string $productName, float $price): bool
{
// ...
```

```php
// Не правильно
/**
 * @param string $productName
 * @param float  $price
 * @return bool
 */
public function incrementProductPriceByName(string $productName, float $price): bool
{
// ...
```

```php
// Правильно
/** 
 * @param array $parsedUrl
 * @phan-param array{scheme:string,host:string,path:string} $parsedUrl
 * @psalm-param array{scheme:string,host:string,path:string} $parsedUrl  
*/
public function showUrl(string $label, array $parsedUrl, string $host): string
{
```

### 2.3. Массивы в docblock

Типы элементов массивов РЕКОМЕНДУЕТСЯ уточнять в docblock.

```php
// Правильно
/**
 * @param string[] $productNames
 */
public function incrementProductPricesByNames(array $productNames, float $price): bool
{
// ...
```

```php
// Не правильно
/**
 * @param array $productNames
 */
public function incrementProductPricesByNames(array $productNames, float $price): bool
{
// ...
```

### 2.4. Неопределенные типы аргументов и возвращаемых результатов

В случае, если аргумент (или возвращаемый результат) метода может быть разных типов НЕОБХОДИМО перечислить все
допустимые типы в docblock.

```php
// Правильно
/**
 * @param string|int $stringOrIntArgument
 * @return float|string|object
 */
public function mixedMethod($stringOrIntArgument)
{
// ...
```

```php
// Не правильно
/**
 * @param mixed $stringOrIntArgument
 * @return mixed
 */
public function mixedMethod($stringOrIntArgument)
{
// ...
```

### 2.5. Тип переменных

Если ожидаемый тип переменной явно не определен НЕОБХОДИМО определить его с помощью однострочного docblock комментария.
Так же необходимо указывать ожидаемый тип, если IDE не может его определить, или определяет не корректно.

```php
$rows = [
    [
        'id'        => 1,
        'createdAt' => new \DateTimeImmutable(),
    ],
    [
        'id'        => 2,
        'createdAt' => new \DateTimeImmutable(),
    ],
    // ...
];

foreach ($rows as $row) {
    /** @var int $id */
    $id = $row['id'];
    /** @var \DateTimeImmutable $createdAt */
    $createdAt = $row['createdAt'];
    // ...
}
```

### 2.6. Свойства

Свойства класса ДОЛЖНЫ содержать docblock, определяющий все возможные типы значений, допустимые в нем.
Если docblock МОЖЕТ быть описан одной строкой — ДОЛЖЕН использоваться однострочный docblock.

```php
/** @var string[]|null */
private $names;

/** @var int|null */
private $count;
```

### 2.7. Методы и функции

Docblock для методов и функций ДОЛЖНЫ быть многострочными.

```php
// Неправильно
/** @param string[] $userNames */
public function saveUserNames(array $userNames): void
```

```php
// Правильно
/**
 * @param string[] $userNames
 */
public function saveUserNames(array $userNames): void
```

## 3. Объявление констант, свойств и методов

### 3.1. Последовательность объявлений констант, свойств и методов

В классе ДОЛЖНА соблюдаться последовательность объявлений элементов согласно следующему списку:

1. Публичные константы.
2. Защищенные константы.
3. Приватные константы.
4. Публичные свойства.
5. Защищенные свойства.
6. Приватные свойства.
7. __construct.
8. __destruct.
9. __clone.
10. __invoke.
11. __toString.
12. Публичные методы.
13. Защищенные методы.
14. Приватные методы.

### 3.2. Именование свойств

Названия свойств ДОЛЖНЫ описывать предназначение данных, которые они хранят.

```php
// Правильно
/** @var string[] */
private $userNames;
```

```php
// Не правильно
/** @var string[] */
private $data;
```

### 3.3. Разделение свойств

Каждое свойство ДОЛЖНО отделяться от других свойств, констант и методов одной пустой строкой.
Если свойство объявляется, как первый элемент класса — пустая строка перед ним НЕДОПУСТИМА.
Если свойство объявляется, как последний элемент класса — пустая строка после него НЕДОПУСТИМА.

```php
// Правильно
/** @var string[] */
private $userNames;

/** @var int[] */
private $userIds;
```

```php
// Не правильно
/** @var string[] */
private $userNames;
/** @var int[] */
private $userIds;
```

```php
// Правильно
{
    /** @var string[] */
    private $userNames;
```

```php
// Не правильно
{

    /** @var string[] */
    private $userNames;
```

```php
// Правильно
    /** @var string[] */
    private $userNames;
}
```

```php
// Не правильно
    /** @var string[] */
    private $userNames;

}
```

### 3.4. Модификаторы доступа для свойств

Для модификаторов доступа к свойствам ДОЛЖНЫ выполняться следующие правила:

* `private` - СЛЕДУЕТ использовать по умолчанию;
* `protected` - СЛЕДУЕТ использоваться только для случаев доступа из дочерних классов;
* `public` - использование НЕДОПУСТИМО;
* `static` - использование НЕДОПУСТИМО.

### 3.5. Именование методов

Названия методов ДОЛЖНЫ описывать предназначение их использования внешним кодом, а не детали реализации.

```php
// Правильно
public function findUserById(int $id): ?User
```

```php
// Не правильно
public function find(int $id): ?User
```

### 3.6. Разделение методов

Каждый метод ДОЛЖЕН отделяться от других методов, свойств и констант одной пустой строкой.
Если метод объявляется, как первый элемент класса — пустая строка перед ним НЕДОПУСТИМА.
Если метод объявляется, как последний элемент класса — пустая строка после него НЕДОПУСТИМА.

```php
// Правильно
public function findUserById(int $id): ?User
// ...
}

public function findUserByName(string $name): ?User
// ...
}
```

```php
// Не правильно
public function findUserById(int $id): ?User
// ...
}
public function findUserByName(string $name): ?User
// ...
}
```

```php
// Правильно
{
    public function findUserById(int $id): ?User
```

```php
// Не правильно
{

    public function findUserById(int $id): ?User
```

```php
// Правильно
    public function findUserById(int $id): ?User
}
```

```php
// Не правильно
    public function findUserById(int $id): ?User

}
```

### 3.7. Модификаторы доступа для методов

Для модификаторов доступа к свойствам ДОЛЖНЫ выполняться следующие правила:

* `private` - СЛЕДУЕТ использовать для методов, предназначенных для использования внутри класса;
* `protected` - СЛЕДУЕТ использоваться только для случаев доступа из дочерних классов;
* `public` - СЛЕДУЕТ использовать для методов, которые предназначены для использования из вне;
* `static` - использование НЕДОПУСТИМО.

### 3.8. Порядок аргументов в методе

Аргументы метода ДОЛЖНЫ объявляться в следующей последовательности:

1. Типизированные аргументы.
2. Nullable-аргументы.
3. Опциональные аргументы.
4. Аргумент с `...`.

```php
public function firstExample(string $first, ?int $second, bool $third = false, float ...$fourth): string
// ...
public function secondExample(?int $second, bool $third = false, float ...$fourth): string
// ...
public function thirdExample(bool $third = false, float ...$fourth): string
```

### 3.9. Массив в виде аргумента

Для методов, содержащих один и более аргументов с типом массив РЕКОМЕНДУЕТСЯ указывать хотя бы один такой аргумент
с помощью оператора `...`.

```php
// Правильно
public function concatStrings(string ...$parts): string
```

```php
// Не правильно
/**
 * @param string $parts
 */
public function concatStrings(array $parts): string
```

## 4. Безопасность

### 4.1. Неявные приведения типов

Неявное приведение типов НЕДОПУСТИМО.

> Неявное приведение типов — один из наиболее распространенных источников ошибок.
> Проблемы, возникающие при неявном приведении типов сложно отслеживать,
> так же они могут приводить к не предсказуемым последствиям.

```php
echo 5 + '5abc5';
// 10
```

### 4.2. Сравнения с преобразованием типов

Сравнения с преобразованием типов `==` и `!=` НЕДОПУСТИМЫ.
Вместо этого НЕОБХОДИМО использовать тождественные сравнения: `===` и `!==`.

> Проблемы тут те же, что и при неявном приведении типов.

```php
if ('abc' == 0) {
    echo 'wat';
}

// wat
```

### 4.3. Инструкция switch

Использовать инструкцию `switch` НЕОБХОДИМО с гарантией корректности типов каждого проверяемого выражения.

> Инструкция `switch` при выполнении проверок `case` использует сравнения с приведением типов.
> Это может привести к тем же проблемам, что и неявное приведение типов.

```php
switch ('abc') {
    case 0:
        echo 'wat';

        break;
}

// wat
```

### 4.4. Присвоения в условных операциях

Присвоение в условиях инструкций `if`, `while`, `do-while` НЕДОПУСТИМО.

> В большом количестве учебной литературы используются конструкции вида `while ($row = ...)` или `if ($row = ...)`.
> Выражения в скобках неявно приводятся к `bool`, что может привести к неожиданным последствиям.

```php
$rows = [0, null, ''];

while ($row = next($rows)) {
    printf("\$row = %s\n", var_dump($row, true));
}

// Ничего не выведет
```

### 4.5. Ошибки

Создание ошибок с помощью `trigger_error` НЕДОПУСТИМО, вместо этого ДОЛЖНЫ использоваться исключения.

> Ошибки могут быть перехвачены только глобально, с помощью `set_error_handler`.
> Это значит, что контекст выполнения будет потерян.
> Так же ошибки не содержат stack trace, в отличие от исключений.

### 4.6. Оператор управления ошибками @

Оператор `@` ДОЛЖЕН быть использован для выражений, которые могут бросить ошибку,
для остальных ситуаций его использование НЕДОПУСТИМО.
В случае подавления ошибки ДОЛЖНО быть брошено исключение с описанием причин возникновения ошибки.

```php
// Без @ будет ошибка:
// Warning: fopen(path/to/not/exists/file): failed to open stream: No such file or directory
$file = @fopen('path/to/not/exists/file', 'r');

if ($file === false) {
    throw new \RuntimeException('Could not open file: "path/to/not/exists/file"');
}
```

### 4.7. goto

Использование инструкции `goto` НЕДОПУСТИМО.

> Оператор `goto` используется для перехода в другую часть программы, чем усложняет чтение и понимание кода.

### 4.8. eval

Использование инструкции `eval` НЕДОПУСТИМО.

> Для безопасного выполнения `eval` необходимо выполнить очень детальный анализ кода, который будет выполняться.
> Сложность требуемых проверок растет экспоненциально с операциями, ожидаемыми для выполнения в `eval`.

### 4.9. Глобальные переменные и global

Использование инструкции `global` НЕДОПУСТИМО.

> Глобальные переменные являются неявными аргументами функции, или метода, не гарантирующими ни тип, ни значение,
> ни даже своего существования.

### 4.10. Статические свойства

Использование статических свойств НЕДОПУСТИМО.

> Статические свойства, по аналогии с глобальными переменным являются неявными аргументами функции, или метода, не
> гарантирующими ни тип, ни корректного состояния.

### 4.11. Суперглобальные переменные

Использование суперглобальных переменных ДОЛЖНО быть сведено к минимуму.
Данные из суперглобальных переменных РЕКОМЕНДУЕТСЯ получать на этапе инициализации.

### 4.12. Динамическая подстановка имен

Динамическая подстановка имен переменных, свойств, функций и методов НЕДОПУСТИМА.

> Динамическая подстановка имен сильно усложняет чтение и отладку кода потому, что конечные имена определяются только
> в рантайме.

```php
// Не правильно
$this->{$methodName}($argument);
```

### 4.13. Магические методы

Использование следующих магических методов НЕДОПУСТИМО:

* `__call`
* `__callStatic`
* `__get`
* `__set`

> Данные методы усложняют чтение и понимание кода, как следствие его поддержку.

### 4.14. Валидация аргументов

Каждый аргумент публичного метода, защищенного метода, или функции ДОЛЖЕН быть проверен на корректность типа и граничные
значения.
Каждый аргумент приватного метода ДОЛЖЕН быть проверен на корректность типа, проверять граничные значения РЕКОМЕНДУЕТСЯ.
Если аргумент не валиден — штатное выполнение метода (функции) невозможно, по этой причине ДОЛЖНО быть брошено
исключение.

### 4.15. \DateTime

Вместо `\DateTime` НЕОБХОДИМО использовать `\DateTimeImmutable`.

> Так как в PHP объекты передаются по ссылке изменение объекта `\DateTime` в одной части кода влечет за собой изменение
> по всему рантайму, что может привести к не предсказуемым последствиям. Что бы исключить целый класс ошибок, связанных
> с не явным изменением даты/времени из внешнего кода НЕОБХОДИМО использовать `\DateTimeImmutable`.

```php
$externalServiceGenerateExpiredAt = function (\DateTime $createdAt): \DateTime {
    return $createdAt->modify('3 days');
};

$createdAt = new \DateTime('2019-01-01');
$expiredAt = $externalServiceGenerateExpiredAt($createdAt);

printf("createdAt: %s, expiredAt: %s", $createdAt->format('Y-m-d'), $expiredAt->format('Y-m-d'));

// createdAt: 2019-01-04, expiredAt: 2019-01-04
```

### 4.16. Обработка часовых поясов

Для задач хранения и обработки времени НЕОБХОДИМО использовать часовой пояс `UTC`.
Для задач связанных с выводом МОЖНО использовать произвольный часовой пояс.

> В случае хранения или обработки времени со смещением по часовому поясу есть большая вероятность возникновения ошибок
> связанных с несоответствием часовых поясов.

### 4.17. SQL

Для подстановки параметров в SQL запросы НЕОБХОДИМО использовать
[псевдопеременные](https://www.php.net/manual/ru/pdo.prepared-statements.php).

> Подстановка параметров с помощью конкатенации ведет к целому классу проблем безопасности: sql-инъекции.

## 5. Принципы программирования

### 5.1. Здравый Смысл

Принцип Здравого Смысла разрешает отмену любого правила данных рекомендаций, в случае, когда правило приводит к
чрезмерному усложнению поддержки кода.
Этот принцип МОЖНО использовать, но очень осторожно.

### 5.2. YAGNI

РЕКОМЕНДУЕТСЯ следовать принципу YAGNI.

### 5.3. SOLID

Код ДОЛЖЕН следовать принципам SOLID.

### 5.4. DRY

Принципу DRY СЛЕДУЕТ придерживаться только в случае, когда он не противоречит SOLID и Здравому смыслу.

> Примеры, когда не стоит следовать принципу DRY:
>
> * У вас есть две разных сущности, отвечающие разным доменам с некой общей функциональностью.
>   В такой ситуации не стоит наследовать сущности одну от другой, или общую функциональность выносить в абстрактный
>   класс, или трейт. Дело в том, что общая функциональность является общей только в текущий момент времени, в будущем
>   же она может измениться в каждом домене по своему. Фактически вам придется в общей функциональности реализовывать
>   ее разделение, в зависимости от домена.
>
> * В тестах DRY может привести к ложно позитивным и ложно негативным ошибкам.

### 5.5. KISS

Принципу KISS СЛЕДУЕТ придерживаться только в случае, когда он не противоречит другим правилам данных рекомендаций.

> Примеры, когда не стоит следовать принципу KISS:
>
> * Класс должен быть "не большого размера". Если придерживаться этого правила - в результате у вы усложните
>   взаимодействие между вашими объектами, что может привести к существенному увеличению сложности в поддержке кода.
>   По этой причине класс должен полностью описывать объект реального мира, которому он соответствует.
>
> * Методы должны быть "не большого размера". Здесь проблемы те же, что и у классов. Разделяя метод на множество
>   маленьких вы расширяете интерфейс класса, что в будущем может привести к излишней связанности, как с данным классом,
>   так и с его наследниками.

### 5.6. TMTOWTDI

Принцип TMTOWTDI НЕ РЕКОМЕНДУЕТСЯ использовать.

> Множество способов реализации одного и того же алгоритма ведет к тому, что правки алгоритма придется выполнять в
> каждой реализации, что в свою очередь усложняет поддержку и увеличивает вероятность ошибок.

### 5.7. GRASP

РЕКОМЕНДУЕТСЯ следовать принципам GRASP.

## 6. Антишаблоны проектирования

## 6.1. ActiveRecord

`ActiveRecord` РЕКОМЕНДУЕТСЯ считать антишаблоном и не использовать его. Вместо этого РЕКОМЕНДУЕТСЯ использовать
шаблон `Repository`.

> ActiveRecord объединяет сущности, представляющие домен вместе с инфраструктурой, в виде логики работы с базой данных.
> Такое поведение нарушает принципы SRP и ISP из SOLID, и приводит к следующим последствиям.
>
>  * Усложнение unit тестирования, так как требует менять поведение подключения к базе данных.
>  * Потеря контроля над тем, у каких модулей использующих сущность должен быть доступ к базе данных, а у каких нет.
>  * Увеличение количества зависимостей от модели и, как следствие, изменяемого объема кода, при правках модели.

## 6.2. Singleton

`Singleton` РЕКОМЕНДУЕТСЯ считать антишаблоном и не использовать его. Вместо этого РЕКОМЕНДУЕТСЯ использовать
`Dependency Ingection`.

> Проблема `Singleton` заключается в том, что состояние объекта, как правило, хранится в статическом свойстве, и
> является не явным аргументом метода, или функции, см. пункт `4.10.` данных рекомендаций.

## 7. Тестирование

### 7.1. Покрытие кода

Каждый метод (функция) ДОЛЖНЫ быть покрыты тестами для всех возможных вариантов выполнения метода (функции).

```php
// Для данного метода ДОЛЖНО быть 3 теста.
// 1. Число $number кратно $divider, что бы проверить корректность преобразование типа.
// Например `divide(4, 2);`.
// 2. Число $number не кратно $divider. Например `divide(1, 2);`.
// 3. Число $divider равно 0. Например `divide(3, 0);`.
public function divide(int $number, int $divider): float.
{
    if ($divider === 0) {
        throw new \InvalidArgumentException('Argument "$divider" must be not zero');
    }

    return (float) $number / $divider;
}

// Для данного метода ДОЛЖНО быть 4 теста.
// 1. Название команды соответствует `self::FIRST_COMMAND`.
// 2. Название команды соответствует `self::SECOND_COMMAND`.
// 3. Название команды - пустая строка.
// 4. Команда не найдена.
public function execute(string $commandName): void
{
    if (empty($commandName)) {
        throw new \InvalidArgumentException('Argument "$commandName" must be not empty');
    }

    switch ($commandName) {
        case self::FIRST_COMMAND:
            $this->firstCommand();

            break;
        case self::SECOND_COMMAND:
            $this->secondCommand();

            break;
        default:
            throw new \DomainException(sprintf('Unknown command: "%s"', $commandName));
    }
}
```

### 7.2. Стратегия тестирования

Код ТРЕБУЕТСЯ покрывать, согласно "белому ящику". В случае чрезмерной сложности использования "белого ящика" СЛЕДУЕТ
использовать стратегию "черного ящика".

### 7.3. Разделение тест методов

Каждый тест метод ДОЛЖЕН иметь полностью независимое состояние, относительно других тест методов.
Каждый тест метод ДОЛЖЕН проверять конкретное поведение тестируемого метода (функции), тест методы, которые проверяют
несколько аспектов поведения НЕДОПУСТИМЫ.

> Принцип DRY для тестов не применяется, что бы минимизировать ложно позитивные и ложно негативные результаты.

### 7.4. Тестируемый объект

Тестируемый объект ТРЕБУЕТСЯ создавать с помощью оператора `new`. В случае невозможности, или чрезмерной сложности теста
ДОПУСКАЕТСЯ использовать mock от тестируемого класса.
Название для объекта СЛЕДУЕТ использовать то же, что и название тестируемого класса, в lowerCamelCase.

### 7.5. Проверка результатов

Проверку результатов НЕОБХОДИМО выполнять на тождество, т.е. и на тип и на значение.
Числа с плавающей точкой ДОЛЖНЫ проверяться с учетом погрешности.
Значения времени, зависящие от текущего времени ДОЛЖНЫ проверяться с учетом погрешности.

## 8. PHPUnit

```php
<?php
// Service/UserRegistrator.php 

declare(strict_types = 1);

namespace Vendor\Project\Service;

use Doctrine\ORM\EntityManagerInterface;
use Psr\Log\LoggerInterface;
use Symfony\Component\Security\Core\Encoder\PasswordEncoderInterface;
use Symfony\Component\Security\Core\User\User;
use Symfony\Component\Security\Core\User\UserInterface;

class UserRegistrator
{
    /** @var PasswordEncoderInterface */
    private $passwordEncoder;

    /** @var LoggerInterface */
    private $logger;

    /** @var string */
    private $salt;

    public function __construct(PasswordEncoderInterface $passwordEncoder, LoggerInterface $logger, string $salt)
    {
        if (empty($salt)) {
            throw new \InvalidArgumentException('Variable "$salt" must be not empty');
        }

        $this->passwordEncoder = $passwordEncoder;
        $this->logger          = $logger;
        $this->salt            = $salt;
    }

    public function register(EntityManagerInterface $entityManager, string $userName, string $password): UserInterface
    {
        if (preg_match('/^[a-z][a-z0-9_]{5,254}$/i', $userName)) {
            throw new \InvalidArgumentException(
                sprintf('Variable "$userName" is invalid, actual value: "%s"', $userName)
            );
        } elseif (empty($password)) {
            throw new \InvalidArgumentException('Variable "$password" must be not empty');
        }

        $this->logger->info(sprintf('Register user: "%s"', $userName));

        try {
            $encodedPassword = $this->passwordEncoder->encodePassword($password, $this->salt);
            $user            = new User($userName, $encodedPassword);

            $entityManager->persist($user);
            $entityManager->flush();

            return $user;
        } catch (\Throwable $exception) {
            $this->logger->error($exception->getMessage(), ['exception' => $exception]);

            throw $exception;
        }
    }
}

```

```php
<?php
// Tests/Service/UserRegistratorTest.php 

declare(strict_types = 1);

namespace Vendor\Project\Tests\Service;

use Doctrine\ORM\EntityManagerInterface;
use PHPUnit\Framework\MockObject\MockObject;
use PHPUnit\Framework\TestCase;
use Psr\Log\LoggerInterface;
use Symfony\Component\Security\Core\Encoder\PasswordEncoderInterface;
use Symfony\Component\Security\Core\User\UserInterface;
use Vendor\Project\Service\UserRegistrator;

class UserRegistratorTest extends TestCase
{
    public function testConstructorWithEmptySalt(): void
    {
        $this->expectException(\InvalidArgumentException::class);
        $this->expectExceptionMessage('Variable "$salt" must be not empty');

        $salt = '';

        /** @var PasswordEncoderInterface|MockObject $passwordEncoder */
        $passwordEncoder = $this->createMock(PasswordEncoderInterface::class);
        /** @var LoggerInterface|MockObject $logger */
        $logger = $this->createMock(LoggerInterface::class);

        new UserRegistrator($passwordEncoder, $logger, $salt);
    }

    public function testRegister(): void
    {
        $salt            = 'salt';
        $userName        = 'userName';
        $password        = 'password';
        $encodedPassword = 'encodedPassword';

        /** @var PasswordEncoderInterface|MockObject $passwordEncoder */
        $passwordEncoder = $this->createMock(PasswordEncoderInterface::class);
        /** @var LoggerInterface|MockObject $logger */
        $logger = $this->createMock(LoggerInterface::class);

        /** @var EntityManagerInterface|MockObject $entityManager */
        $entityManager = $this->createMock(EntityManagerInterface::class);

        $userRegistrator = new UserRegistrator($passwordEncoder, $logger, $salt);

        $entityManagerIncrement = 0;

        $logger
            ->expects($this->once())
            ->method('info')
            ->with(sprintf('Register user: "%s"', $userName));

        $passwordEncoder
            ->expects($this->once())
            ->method('encodePassword')
            ->with($password, $salt)
            ->willReturn($encodedPassword);

        $entityManager
            ->expects($this->at($entityManagerIncrement++))
            ->method('persist')
            ->with(
                $this->callback(
                    function (UserInterface $user) use ($encodedPassword, $userName): bool {
                        $this->assertSame($userName, $user->getUsername());
                        $this->assertSame($encodedPassword, $user->getPassword());

                        return true;
                    }
                )
            );

        /** @noinspection PhpUnusedLocalVariableInspection */
        $entityManager
            ->expects($this->at($entityManagerIncrement++))
            ->method('flush');

        $logger
            ->expects($this->never())
            ->method('error');

        $user = $userRegistrator->register($entityManager, $userName, $password);

        $this->assertSame($userName, $user->getUsername());
        $this->assertSame($encodedPassword, $user->getPassword());
    }

    public function testRegisterWithInvalidUserName(): void
    {
        $this->expectException(\InvalidArgumentException::class);
        $this->expectExceptionMessage('Variable "$userName" is invalid, actual value: "*"');

        $salt     = 'salt';
        $userName = '*';
        $password = 'password';

        /** @var PasswordEncoderInterface|MockObject $passwordEncoder */
        $passwordEncoder = $this->createMock(PasswordEncoderInterface::class);
        /** @var LoggerInterface|MockObject $logger */
        $logger = $this->createMock(LoggerInterface::class);

        /** @var EntityManagerInterface|MockObject $entityManager */
        $entityManager = $this->createMock(EntityManagerInterface::class);

        $userRegistrator = new UserRegistrator($passwordEncoder, $logger, $salt);

        $logger
            ->expects($this->never())
            ->method('info');

        $passwordEncoder
            ->expects($this->never())
            ->method('encodePassword');

        $entityManager
            ->expects($this->never())
            ->method('persist');

        $entityManager
            ->expects($this->never())
            ->method('flush');

        $logger
            ->expects($this->never())
            ->method('error');

        $userRegistrator->register($entityManager, $userName, $password);
    }

    public function testRegisterWithInvalidPassword(): void
    {
        $this->expectException(\InvalidArgumentException::class);
        $this->expectExceptionMessage('Variable "$password" must be not empty');

        $salt     = 'salt';
        $userName = 'userName';
        $password = '';

        /** @var PasswordEncoderInterface|MockObject $passwordEncoder */
        $passwordEncoder = $this->createMock(PasswordEncoderInterface::class);
        /** @var LoggerInterface|MockObject $logger */
        $logger = $this->createMock(LoggerInterface::class);

        /** @var EntityManagerInterface|MockObject $entityManager */
        $entityManager = $this->createMock(EntityManagerInterface::class);

        $userRegistrator = new UserRegistrator($passwordEncoder, $logger, $salt);

        $logger
            ->expects($this->never())
            ->method('info');

        $passwordEncoder
            ->expects($this->never())
            ->method('encodePassword');

        $entityManager
            ->expects($this->never())
            ->method('persist');

        $entityManager
            ->expects($this->never())
            ->method('flush');

        $logger
            ->expects($this->never())
            ->method('error');

        $userRegistrator->register($entityManager, $userName, $password);
    }

    public function testRegisterWithUnexpectedDbException(): void
    {
        $this->expectException(\Exception::class);
        $this->expectExceptionMessage('UnexpectedException');

        $salt            = 'salt';
        $userName        = 'userName';
        $password        = 'password';
        $encodedPassword = 'encodedPassword';
        $exception       = new \Exception('UnexpectedException');
        $logContext      = ['exception' => $exception];

        /** @var PasswordEncoderInterface|MockObject $passwordEncoder */
        $passwordEncoder = $this->createMock(PasswordEncoderInterface::class);
        /** @var LoggerInterface|MockObject $logger */
        $logger = $this->createMock(LoggerInterface::class);

        /** @var EntityManagerInterface|MockObject $entityManager */
        $entityManager = $this->createMock(EntityManagerInterface::class);

        $userRegistrator = new UserRegistrator($passwordEncoder, $logger, $salt);

        $entityManagerIncrement = 0;

        $logger
            ->expects($this->once())
            ->method('info')
            ->with(sprintf('Register user: "%s"', $userName));

        $passwordEncoder
            ->expects($this->once())
            ->method('encodePassword')
            ->with($password, $salt)
            ->willReturn($encodedPassword);

        $entityManager
            ->expects($this->at($entityManagerIncrement++))
            ->method('persist')
            ->with(
                $this->callback(
                    function (UserInterface $user) use ($encodedPassword, $userName): bool {
                        $this->assertSame($userName, $user->getUsername());
                        $this->assertSame($encodedPassword, $user->getPassword());

                        return true;
                    }
                )
            );

        /** @noinspection PhpUnusedLocalVariableInspection */
        $entityManager
            ->expects($this->at($entityManagerIncrement++))
            ->method('flush')
            ->willThrowException($exception);

        $logger
            ->expects($this->once())
            ->method('error')
            ->with($exception->getMessage(), $logContext);

        $userRegistrator->register($entityManager, $userName, $password);
    }
}

```

### 8.1. Именование тестовых классов

Тестовый класс ДОЛЖЕН состоять из префикса `Test` и названия тестируемого класса.

### 8.1. Именование тест методов

Тестовый метод ДОЛЖЕН начинаться с префикса `test`, далее указывается название тестируемого метода в `UpperCamelCase`.
Тест без дополнительных аспектов в названии ДОЛЖЕН считаться позитивным.
Для описания дополнительных аспектов в названии тестового метода СЛЕДУЕТ использовать префиксы `With` и `Without`.
Множество дополнительных аспектов разделяется с помощью строки `And`.

```php
public function testLogMessage(): void
// ...
public function testLogMessageWithEmptyMessage(): void
// ...
public function testLogMessageWithEmptyMessageAndEmtyContext(): void
// ...
public function testLogMessageWithInvalidContext(): void
```

### 8.2. Структура теста

Каждый тест ТРЕБУЕТСЯ оформлять согласно структуре, описанной ниже (каждый блок отделяется от остальных пустой строкой).

1. Ожидаемый тип исключения.
2. Ожидаемое сообщение исключения.
3. Переменные, используемые в тесте.
4. Mock-объекты аргументов конструктора тестируемого класса.
5. Mock-объекты аргументов тестируемого метода.
6. Создание тестируемого объекта.
7. Инкременты вызовов mock-объектов.
8. Поведение методов mock-объектов согласно порядку их вызова.
9. Вызов тестируемого метода.
10. Проверка результатов.

ДОПУСКАЕТСЯ отклонение от данной структуры, в случае, если полное следование ей невозможно. Например, когда значение
переменной [3] определяется только после вызова конструктора тестируемого класса [6].

### 8.3. Переменные, используемые в тесте

Переменные, используемые в тесте ДОЛЖНЫ следовать следующим правилам.

1. НЕДОПУСТИМО использовать свойства тест классов.
2. Значения, которые будут использоваться отдельно ДОЛЖНЫ быть вынесены в отдельные переменные.
3. Значения для переменных ТРЕБУЕТСЯ указывать явно.
4. Значения для переменных НЕ ДОЛЖНЫ зависеть от времени, кроме ситуаций, когда тестируемый метод зависит от текущего
времени.

### 8.4. Mock-объекты

Mock-объект ДОЛЖЕН быть объявлен, согласно следующим правилам.

1. Переменную, содержащая mock-объект СЛЕДУЕТ называть согласно названию аргумента метода (функции), где будет
использоваться данный объект.
2. Mock-объект ДОЛЖЕН быть помечен строчным docblock, содержащими класс объекта, для которого создается mock и
mock-интерфейс.
3. Mock-объект ДОЛЖЕН присваиваться переменной тестового метода.

```php
/** @var PasswordEncoderInterface|MockObject $passwordEncoder */
$passwordEncoder = $this->createMock(PasswordEncoderInterface::class);
/** @var LoggerInterface|MockObject $logger */
$logger = $this->createMock(LoggerInterface::class);
```

### 8.5. Инкременты вызовов mock-объектов

Инкременты вызовов mock-объектов - это переменные типа `int`, со значением 0.
Названия для этих переменных ДОЛЖНЫ повторять названия mock-объектов, которым они соответствуют с суффиксом `Increment`.
Инкременты ДОЛЖНЫ использоваться, когда необходимо описать последовательность вызовов методов mock-объекта.

### 8.6. Поведение методов mock-объектов

Поведение методов mock-объектов ДОЛЖНО описываться согласно одной из следующих структур.

1. Метод `methodName` mock-объекта `$mockObject` НЕ ДОЛЖЕН быть вызван.

```php
$mockObject
    ->expects($this->never())
    ->method('methodName');
```

2. Метод `methodName` mock-объекта `$mockObject` ДОЛЖЕН быть вызван с аргументами `$methodArguments` и вернуть
результат.

```php
$mockObject
    ->expects($this->once())    // Или `->expects($this->at($mockObjectIncrement++))`
    ->method('methodName')
    ->with(...$methodArguments)
    ->willReturn($methodResult) // Или `->willReturnSelf();`
```

3. Метод `methodName` mock-объекта `$mockObject` ДОЛЖЕН быть вызван один раз без аргументов и вернуть результат.

```php
$mockObject
    ->expects($this->once())    // Или `->expects($this->at($mockObjectIncrement++))`
    ->method('methodName')
    ->willReturn($methodResult) // Или `->willReturnSelf();`
```

4. Метод `methodName` mock-объекта `$mockObject` ДОЛЖЕН быть вызван с аргументами `$methodArguments` и бросить
исключение `$exception`.

```php
$mockObject
    ->expects($this->once())    // Или `->expects($this->at($mockObjectIncrement++))`
    ->method('methodName')
    ->with(...$methodArguments)
    ->willThrowException($exception);
```

5. Метод `methodName` mock-объекта `$mockObject` ДОЛЖЕН быть вызван один раз без аргументов и бросить исключение
`$exception`.

```php
$mockObject
    ->expects($this->once()) // Или `->expects($this->at($mockObjectIncrement++))`
    ->method('methodName')
    ->willThrowException($exception);
```

### 8.7 Порядок утверждений для одного значения

В случае когда для проверки одного значения требуется несколько утверждений, эти утверждения ДОЛЖНЫ быть описаны в
порядке от максимально информативных до минимально информативных, далее от общих к частным.

```php
// Правильно
/** @var JsonResponse|Response $response */
$response = $action->run(/* ... */);

$this->assertSame($expectedContent, $response->getContent());
$this->assertSame(Response::HTTP_OK, $response->getStatusCode());
$this->assertInstanceOf(JsonResponse::class, $response);
```

```php
// Не правильно
// В случае возникновения ошибки не будет ясно, что же за ошибка произошла, вместо этого получим только несоответствие
// типа $response, или статус кода.
/** @var JsonResponse|Response $response */
$response = $action->run(/* ... */);

$this->assertInstanceOf(JsonResponse::class, $response);
$this->assertSame(Response::HTTP_OK, $response->getStatusCode());
$this->assertSame($expectedContent, $response->getContent());
```

```php
// Правильно
$exceptionContext = $object->method(/* ... */);

$this->assertIsArray($exceptionContext);
$this->assertNotEmpty($exceptionContext);
$this->assertArrayHasKey('exception', $exceptionContext);
$this->assertInstanceOf(\Exception::class, $exceptionContext['exception']);
$this->assertSame($expectedExceptionMessage, $exceptionContext['exception']->getMessage());
```

```php
// Не правильно
$exceptionContext = $object->method(/* ... */);

$this->assertSame($expectedExceptionMessage, $exceptionContext['exception']->getMessage());
```

### 8.8. Проверка утверждений на основании результатов собственных проверок

Проверка утверждений на основании результатов собственных проверок ДОПУСКАЕТСЯ только в случае, когда отсутствует
`assert*` метод, включающий эту проверку. Во всех остальных случая НЕОБХОДИМО использовать `assert*` метод.

> Распространенной ошибкой является "ручная" проверка значения и утверждение о ее ложном, или положительном результате.
> В следствии такого подхода, срабатывание утверждения не покажет информацию о том, что же пошло не так.

```php
// Правильно
$this->assertSame($expectedString, $actualString);

// Не правильно
$this->assertSame(true, $expectedString === $actualString);

// Не правильно
$this->assertTrue($expectedString === $actualString);
```

```php
// Правильно
$this->assertStringStartsWith($expectedPrefix, $actualString);

// Не правильно
$this->assertSame(0, strpos($actualString, $expectedPrefix));
```

```php
// Правильно
$this->assertTrue($actualBool);

// Не правильно
$this->assertTrue($actualBool === true);

// Не правильно
$this->assertSame(true, $actualBool);
```

### 8.9. Проверки значений на основании `TestCase::callback`

Для проверок значений на основании `TestCase::callback` НЕОБХОДИМО использовать утверждения, а не возвращать `false`.

> В случае, когда `TestCase::callback` получает `false`, он теряет информацию о причинах, почему проверка дала ложный
> результат. Поиск этих причин усложняет процесс отладки. Если же вместо проверок с булевым результатом использовать
> утверждения — информация о проблеме не будет потеряна.

```php
// Правильно
$userRepository
    ->expects($this->once())
    ->method('findByGroup')
    ->with(
        $this->callback(
            function (Group $group) use ($groupId, $groupName): bool {
                $this->assertSame($groupId, $group->getId());
                $this->assertSame($groupName, $group->getName());
                
                return true;
            }
        )
    )
    ->willReturn($users);
```

```php
// Не правильно
$userRepository
    ->expects($this->once())
    ->method('findByGroup')
    ->with(
        $this->callback(
            function (Group $group) use ($groupId, $groupName): bool {
                // Если следующая проверка не выполнится, в лог будет добавлено сообщение о том, что аргумент не
                // прошел проверку. Информация о том, какая из частей этой проверки дала ложный результат, и какие
                // в принципе значения сравнивались, будет потеряна.
                return $group->getId() === $groupId && $group->getName() === $groupName;
            }
        )
    )
    ->willReturn($users);
```

### 8.10. Проверка утверждений для числовых значений

Для проверок числовых значений без учета погрешности ДОЛЖЕН использоваться метод `assertSame`.

```php
// Правильно
$expected = 5;
$actual   = 5;

$this->assertSame($expected, $actual);
```

```php
// Не правильно
$expected = 5;
$actual   = 5;

$this->assertEqual($expected, $actual);
```

Для проверок числовых значений с учетом погрешности ДОЛЖЕН использоваться метод `assertEqual` с обязательным указанием
погрешности.

```php
// Правильно
$expected = 5;
$actual   = 4.5;

$this->assertEqual($expected, $actual, '', 1);
```

### 8.11. Проверка утверждений для \DateTimeImmutable

Проверки объектов \DateTimeImmutable ДОЛЖНЫ осуществляться на основании `timestamp`, а не сравнения объектов.
Для проверок \DateTimeImmutable, не зависящих от текущего времени ДОЛЖЕН использоваться метод `assertSame`.

```php
$expected = new \DateTimeImmutable('2019-01-01 10:20:30');
$actual   = new \DateTimeImmutable('2019-01-01 10:20:30');

$this->assertSame($expected->getTimestamp(), $actual->getTimestamp());
```

Для проверок \DateTimeImmutable зависящих от текущего времени ДОЛЖЕН использоваться метод `assertEqual` с обязательным
указанием погрешности.

```php
$expected = new \DateTimeImmutable();
$actual   = new \DateTimeImmutable();

$this->assertEqual($expected->getTimestamp(), $actual->getTimestamp(), '', 2);
```

> В случае проверок данных на основании текущего времени высока вероятность ложно позитивных и ложно негативных
> результатов. Дело в том, что сам процесс выполнения теста требует некоторого времени, как результат это время является
> неявной и не контролируемой переменной в тесте.

## 9. IDE

Для разработки php проектов РЕКОМЕНДУЕТСЯ использовать [PhpStorm](https://www.jetbrains.com/phpstorm/).

### 9.1. Inspections и Code Style

Настройки инспекций РЕКОМЕНДУЕТСЯ [импортировать](https://www.jetbrains.com/help/phpstorm/customizing-profiles.html) из
`phpstorm/php-conventions-inspections.xml`. Данные инспекции используют
[PHP_CodeSniffer](https://www.jetbrains.com/help/phpstorm/using-php-code-sniffer.html).

Настройки код стайла РЕКОМЕНДУЕТСЯ [импортировать](https://www.jetbrains.com/help/phpstorm/configuring-code-style.html)
из `phpstorm/php-conventions-code-style.xml`.

**ВАЖНО** Inspections и Code Style содержат настройки только для PHP, по этой причине СТОИТ выполнять импорт
как расширение схемы, выбрав опцию `Current scheme`.
