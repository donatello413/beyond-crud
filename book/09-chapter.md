## ### Замечание о DTO в PHP 8

В PHP 8 внедрена поддержка **именованных аргументов** (named arguments), а также **перемещения свойств конструктора** (
constructor property promotion). Эти две функции окажут огромное влияние на количество шаблонного кода (boilerplate),
который вам потребуется писать.

Вот как выглядит небольшой класс DTO в PHP 7.4:

```php
class CustomerData extends DataTransferObject
{
    public string $name;
    public string $email;
    public Carbon $birth_date;

    public static function fromRequest(CustomerRequest $request): self {
        return new self([
            'name' => $request->get('name'),
            'email' => $request->get('email'),
            'birth_date' => Carbon::make(
                $request->get('birth_date')
            ),
        ]);
    }
}

$data = CustomerData::fromRequest($customerRequest);
```

В этом примере вам приходится писать значительное количество кода, чтобы определить свойства и сконструировать объект
вручную. В PHP 8 использование новых возможностей позволит сделать этот код намного проще и короче.

Вот как это будет выглядеть в PHP 8. Благодаря нововведениям PHP 8 теперь можно значительно сократить шаблонный код (
boilerplate). Вот пример того же класса DTO, но использующего **перемещение свойств конструктора** (constructor property
promotion):

```php
class CustomerData
{
    public function __construct(
        public string $name,
        public string $email,
        public Carbon $birth_date,
    ) {}
}

$data = new CustomerData(...$customerRequest->validated());
```

### Потому что данные — ключевая часть любого проекта

Данные лежат в основе практически каждого проекта, и потому они являются одним из самых важных элементов. Объекты
передачи данных (Data Transfer Objects, DTO) предоставляют вам способ работы с данными структурированным, типобезопасным
и предсказуемым образом.

Вы заметите, что на протяжении всей этой книги DTO используются довольно часто. Именно поэтому было важно подробно
рассмотреть их уже в самом начале.

Впрочем, существует ещё один ключевой элемент, который заслуживает нашего пристального внимания: **действия** (actions).
Им и будет посвящена следующая глава.