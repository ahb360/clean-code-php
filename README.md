# Clean Code PHP

## فهرست مطالب

  1. [مقدمه](#introduction)
  2. [متغیرها](#variables)
     * [از نام متغیرهایی استفاده کنید که با معنی و قابل بیان کردن باشند](#use-meaningful-and-pronounceable-variable-names)
     * [برای یک نوع متغیر از واژگان یکسان استفاده کنید](#use-the-same-vocabulary-for-the-same-type-of-variable)
     * [از نام‌های قابل جستجو استفاده کنید (بخش ۱)](#use-searchable-names-part-1)
     * [از نام‌های قابل جستجو استفاده کنید (بخش ۲)](#use-searchable-names-part-2)
     * [از متغیرهای توضیحی استفاده کنید](#use-explanatory-variables)
     * [از کدهای تو در تو اجتناب کنید و زود پاسخ را برگردانید (بخش ۱)](#avoid-nesting-too-deeply-and-return-early-part-1)
     * [از کدهای تو در تو اجتناب کنید و زود پاسخ را برگردانید (بخش ۲)](#avoid-nesting-too-deeply-and-return-early-part-2)
     * [از نگاشت ذهنی اجتناب کنید](#avoid-mental-mapping)
     * [متن بلا استفاده ایجاد نکنید](#dont-add-unneeded-context)
     * [از آرگومان‌های پیش فرض به جای آرگومان‌های کوتاه شده یا نا مفهوم استفاده کنید](#use-default-arguments-instead-of-short-circuiting-or-conditionals)
  3. [مقایسه](#comparison)
     * [از مقایسه‌های منطبق استفاده کنید](#use-identical-comparison)
  4. [توابع](#functions)
     * [پارامترهای تابع (در حالت ایده‌آل ۲ یا کمتر باشد)](#function-arguments-2-or-fewer-ideally)
     * [توابع باید یک کار انجام دهند](#functions-should-do-one-thing)
     * [نام توابع باید بگوید که تابع چه کاری انجام می‌دهد](#function-names-should-say-what-they-do)
     * [توابع باید فقط در یک سطح انتزاعی باشند](#functions-should-only-be-one-level-of-abstraction)
     * [از flag به عنوان پارامتر در تابع استفاده نکنید](#dont-use-flags-as-function-parameters)
     * [از تاثیرات جانبی دوری کنید](#avoid-side-effects)
     * [در توابع جانی چیزی ننویسید](#dont-write-to-global-functions)
     * [از الگوی Singleton استفاده نکنید](#dont-use-a-singleton-pattern)
     * [عبارات شرطی را کپسوله سازی کنید](#encapsulate-conditionals)
     * [از عبارات شرطی منفی دوری کنید](#avoid-negative-conditionals)
     * [از عبارات شرطی دوری کنید](#avoid-conditionals)
     * [از چک کردن نوع دوری کنید (بخش ۱)](#avoid-type-checking-part-1)
     * [از چک کردن نوع دوری کنید (بخش ۲)](#avoid-type-checking-part-2)
     * [کد مرده را حذف کنید](#remove-dead-code)
  5. [اشیا و ساختمان داده](#objects-and-data-structures)
     * [از کپسوله سازی شیء استفاده کنید](#use-object-encapsulation)
     * [کاری کنید که اشیاء اعضای private/protected داشته باشند](#make-objects-have-privateprotected-members)
  6. [Classes](#classes)
     * [Prefer composition over inheritance](#prefer-composition-over-inheritance)
     * [Avoid fluent interfaces](#avoid-fluent-interfaces)
     * [Prefer `final` classes](#prefer-final-classes)
  7. [SOLID](#solid)
     * [Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
     * [Open/Closed Principle (OCP)](#openclosed-principle-ocp)
     * [Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
     * [Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
     * [Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)
  8. [Don’t repeat yourself (DRY)](#dont-repeat-yourself-dry)
  9. [Translations](#translations)

## مقدمه

اصول و قواعد مهندسی نرم‌افزار, برگرفته از کتاب
[*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
نوشته رابرت مارتین (Robert C. Martin),
و سازگار شده برای زبان PHP. این راهنمایی برای استایل نوشتن کد نیست. این راهنما به شما کمک می‌کند بوسیله زبان PHP
نرم‌افزارهای خوانا، قابل استفاده مجدد، و قابل اصلاح تولید کنید.

لازم نیست همه قوانین این مطلب را مو به مو اجرا کنید، حتی علما در بسیاری از این قوانین اختلاف نظر دارند.
این‌ها فقط دستورالعمل هستند نه چیز بیشتری. ولی این دستورالعمل‌ها حاصل تجربه نویسندگان *Clean Code* طی سالیان
دراز بوده است.

الهام گرفته شده از [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript).

با وجود اینکه بسیاری از توسعه دهندگان هنوز از PHP 5 استفاده می‌کنند, بسیاری از مثال‌های موجود در این مقاله
فقط در PHP 7.1+ کار می‌کنند.

## متغیرها

### از نام متغیرهایی استفاده کنید که با معنی و قابل بیان کردن باشند

**بد:**

```php
$ymdstr = $moment->format('y-m-d');
```

**خوب:**

```php
$currentDate = $moment->format('y-m-d');
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### برای یک نوع متغیر از واژگان یکسان استفاده کنید

**بد:**

```php
getUserInfo();
getUserData();
getUserRecord();
getUserProfile();
```

**خوب:**

```php
getUser();
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از نام‌های قابل جستجو استفاده کنید (بخش ۱)

ما بیش از اینکه کد بنویسیم، کد میخوانیم. در نتیجه این موضوع که کد ما قابل جستجو و خواندن
باشد اهمیت پیدا می‌کند. اگر متغیرها را به صورتی نامگذاری نکنیم که معنی درستی داشته باشند و
در فهم برنامه کمک کنند. در واقع به کسانی که برنامه ما را می‌خوانند صدمه زده‌ایم.
نام‌های متغیرها را به صورتی انتخاب کنید که قابل جستجو شدن باشند.

**بد:**

```php
// این ۴۸۸ دیگه از کجا اومد؟
$result = $serializer->serialize($data, 448);
```

**خوب:**

```php
$json = $serializer->serialize($data, JSON_UNESCAPED_SLASHES | JSON_PRETTY_PRINT | JSON_UNESCAPED_UNICODE);
```

### از نام‌های قابل جستجو استفاده کنید (بخش ۲)

**بد:**

```php
class User
{
    // این ۷ دیگه از کجا اومد؟
    public $access = 7;
}

// ۴ چی میگه؟
if ($user->access & 4) {
    // ...
}

// اینجا چه خبره؟
$user->access ^= 2;
```

**خوب:**

```php
class User
{
    const ACCESS_READ = 1;
    const ACCESS_CREATE = 2;
    const ACCESS_UPDATE = 4;
    const ACCESS_DELETE = 8;

    // کاربر به صورت پیش فرض میتونه چیزی رو بخونه، ایجاد کنه و بروز رسانی کنه
    public $access = self::ACCESS_READ | self::ACCESS_CREATE | self::ACCESS_UPDATE;
}

if ($user->access & User::ACCESS_UPDATE) {
    // ویرایش رو انجام بده ...
}

// دسترسی برای ایجاد چیزی گرفته شده
$user->access ^= User::ACCESS_CREATE;
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از متغیرهای توضیحی استفاده کنید

**بد:**

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(.+?)\s*(\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches[1], $matches[2]);
```

**بدک نیست:**

الان بهتر شد، ولی همچنان خیلی وابسته به regex هستیم.

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(.+?)\s*(\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

[, $city, $zipCode] = $matches;
saveCityZipCode($city, $zipCode);
```

**خوب:**

با نام گذاری زیرالگوها وابستگی به regex را کم کردیم.

```php
$address = 'One Infinite Loop, Cupertino 95014';
$cityZipCodeRegex = '/^[^,]+,\s*(?<city>.+?)\s*(?<zipCode>\d{5})$/';
preg_match($cityZipCodeRegex, $address, $matches);

saveCityZipCode($matches['city'], $matches['zipCode']);
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از کدهای تو در تو اجتناب کنید و زود پاسخ را برگردانید (بخش ۱)

تعداد زیادی if-else خواندن و دنبال کردن کد شما را می‌تواند سخت کند. همیشه صراحت بهتر از ضمنی بیان کردن است.

**بد:**

```php
function isShopOpen($day): bool
{
    if ($day) {
        if (is_string($day)) {
            $day = strtolower($day);
            if ($day === 'friday') {
                return true;
            } elseif ($day === 'saturday') {
                return true;
            } elseif ($day === 'sunday') {
                return true;
            } else {
                return false;
            }
        } else {
            return false;
        }
    } else {
        return false;
    }
}
```

**خوب:**

```php
function isShopOpen(string $day): bool
{
    if (empty($day)) {
        return false;
    }

    $openingDays = [
        'friday', 'saturday', 'sunday'
    ];

    return in_array(strtolower($day), $openingDays, true);
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از کدهای تو در تو اجتناب کنید و زود پاسخ را برگردانید (بخش ۲)

**بد:**

```php
function fibonacci(int $n)
{
    if ($n < 50) {
        if ($n !== 0) {
            if ($n !== 1) {
                return fibonacci($n - 1) + fibonacci($n - 2);
            } else {
                return 1;
            }
        } else {
            return 0;
        }
    } else {
        return 'Not supported';
    }
}
```

**خوب:**

```php
function fibonacci(int $n): int
{
    if ($n === 0 || $n === 1) {
        return $n;
    }

    if ($n >= 50) {
        throw new \Exception('Not supported');
    }

    return fibonacci($n - 1) + fibonacci($n - 2);
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از نگاشت ذهنی اجتناب کنید

خواننده را مجبور نکنید که برای فهمیدن متغیر آن را ترجمه کند.
همیشه صراحت بهتر از ضمنی بیان کردن است.

**بد:**

```php
$l = ['Austin', 'New York', 'San Francisco'];

for ($i = 0; $i < count($l); $i++) {
    $li = $l[$i];
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    // صبر کن, این `$li` برای چی استفاده می‌شد؟
    dispatch($li);
}
```

**خوب:**

```php
$locations = ['Austin', 'New York', 'San Francisco'];

foreach ($locations as $location) {
    doStuff();
    doSomeOtherStuff();
    // ...
    // ...
    // ...
    dispatch($location);
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### متن بلا استفاده ایجاد نکنید

اگر نام کلاس یا شیء چیزی به شما می‌گوید، مجددا آن را در نام متغیر تکرار نکنید.

**بد:**

```php
class Car
{
    public $carMake;
    public $carModel;
    public $carColor;

    //...
}
```

**خوب:**

```php
class Car
{
    public $make;
    public $model;
    public $color;

    //...
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از آرگومان‌های پیش فرض به جای آرگومان‌های کوتاه شده یا نا مفهوم استفاده کنید

**خوب نیست:**

این خوب نیست چون `$breweryName` می‌تواند `NULL` باشد.

```php
function createMicrobrewery($breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**بد نیست:**

این حالت قابل فهم‌تر از قبلی است، ولی بهتر است مقدار متغیر را هم کنترل کند.

```php
function createMicrobrewery($name = null): void
{
    $breweryName = $name ?: 'Hipster Brew Co.';
    // ...
}
```

**خوب:**

می‌توانید از [type hinting](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration) استفاده کرده و مطمئن شوید که `$breweryName` مقدار `NULL` نخواهد داشت.

```php
function createMicrobrewery(string $breweryName = 'Hipster Brew Co.'): void
{
    // ...
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

## مقایسه

### از [مقایسه‌های منطبق](http://php.net/manual/en/language.operators.comparison.php) استفاده کنید

**خوب نیست:**

یک مقایسه ساده رشته را به عدد تغییر می‌دهد.

```php
$a = '42';
$b = 42;

if ($a != $b) {
   // The expression will always pass
}
```

مقایسه `$a != $b` جواب `FALSE` را بر می‌گرداند ولی در واقع `TRUE` است!
رشته `42` با عدد صحیح `42` یکی نیستند.

**خوب:**

مقایسه منطبق هم نوع و هم مقدار را با هم مقایسه می‌کند.

```php
$a = '42';
$b = 42;

if ($a !== $b) {
    // The expression is verified
}
```

مقایسه `$a !== $b` جواب `TRUE` را برمی‌گرداند.

**[⬆ بازگشت به بالا](#table-of-contents)**


## توابع

### پارامترهای تابع (در حالت ایده‌آل ۲ یا کمتر باشد)

محدود کردن پارامترهای تابع بسیار مهم است به این دلیل که تست کردن تابع را ساده‌تر می‌کند.
بیش از ۳ پارامتر باعثت انفجار جایگشت‌ها شده و در نتیجه شما باید حالت‌های زیادی را با
هر پارامتر تست کنید.

توابع بدون پارامتر حالت ایده‌آل هستند. یک یا دو پارامتر اشکال ندارد، و از ۳ پارامتر باید
دوری کرد. هر چیز بیشتری از آن را باید ترکیب کرد. معمولا اگر بیش از دو پارامتر داشته باشیم
تابع ما سعی دارد کار زیادی را انجام دهد. در حالتی که اینگونه نیست، بیشتر مواقع یک شیء
سطح بالا به عنوان یک پارامتر کافی است.

**بد:**

```php
function createMenu(string $title, string $body, string $buttonText, bool $cancellable): void
{
    // ...
}
```

**خوب:**

```php
class MenuConfig
{
    public $title;
    public $body;
    public $buttonText;
    public $cancellable = false;
}

$config = new MenuConfig();
$config->title = 'Foo';
$config->body = 'Bar';
$config->buttonText = 'Baz';
$config->cancellable = true;

function createMenu(MenuConfig $config): void
{
    // ...
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### توابع باید یک کار انجام دهند

تا الان این مورد مهم‌ترین قانون در مهندسی نرم افزار بوده. وقتی توابع بیش از یک کار انجام
می‌دهند، ساختن، تست و دلی آوردن در مورد آنها سخت تر می‌شود. وقتی ب‌توانید یک تابع را طوری
ایزوله کنید که فقط یک کار انجام دهد، اصلاح کردن آن ساده‌تر می‌شود و کد شما تمیزتر
خواهد بود. اگر هیچ چیزی از این راهنما یاد نگیرید و فقط این مورد را متوجه شوید و استفاده
کنید، از بسیاری از دولوپرها جلوتر خواهید بود.

**بد:**
```php
function emailClients(array $clients): void
{
    foreach ($clients as $client) {
        $clientRecord = $db->find($client);
        if ($clientRecord->isActive()) {
            email($client);
        }
    }
}
```

**خوب:**

```php
function emailClients(array $clients): void
{
    $activeClients = activeClients($clients);
    array_walk($activeClients, 'email');
}

function activeClients(array $clients): array
{
    return array_filter($clients, 'isClientActive');
}

function isClientActive(int $client): bool
{
    $clientRecord = $db->find($client);

    return $clientRecord->isActive();
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### نام توابع باید بگوید که تابع چه کاری انجام می‌دهد

**بد:**

```php
class Email
{
    //...

    public function handle(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// What is this? A handle for the message? Are we writing to a file now?
$message->handle();
```

**خوب:**

```php
class Email
{
    //...

    public function send(): void
    {
        mail($this->to, $this->subject, $this->body);
    }
}

$message = new Email(...);
// Clear and obvious
$message->send();
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### توابع باید فقط در یک سطح انتزاعی باشند

وقتی بیش از یک سطح انتزاع دارید تابع شما معمولا کارهای زیادی انجام می‌دهد. تکه تکه
کردن تابع منجر به ایجاد قابلیت استفاده مجدد و تست ساده‌تر خواهد شد.

**بد:**

```php
function parseBetterJSAlternative(string $code): void
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            // ...
        }
    }

    $ast = [];
    foreach ($tokens as $token) {
        // lex...
    }

    foreach ($ast as $node) {
        // parse...
    }
}
```

**باز هم بد:**

ما بخشی از عملکرد تابع را خارج کدیم ولی هنوز `parseBetterJSAlternative()` خیلی
پیچیده و غیر قابل تست است.

```php
function tokenize(string $code): array
{
    $regexes = [
        // ...
    ];

    $statements = explode(' ', $code);
    $tokens = [];
    foreach ($regexes as $regex) {
        foreach ($statements as $statement) {
            $tokens[] = /* ... */;
        }
    }

    return $tokens;
}

function lexer(array $tokens): array
{
    $ast = [];
    foreach ($tokens as $token) {
        $ast[] = /* ... */;
    }

    return $ast;
}

function parseBetterJSAlternative(string $code): void
{
    $tokens = tokenize($code);
    $ast = lexer($tokens);
    foreach ($ast as $node) {
        // parse...
    }
}
```

**خوب:**

بهترین راهکار خارج کردن وابستگی‌های تابع `parseBetterJSAlternative()` است.

```php
class Tokenizer
{
    public function tokenize(string $code): array
    {
        $regexes = [
            // ...
        ];

        $statements = explode(' ', $code);
        $tokens = [];
        foreach ($regexes as $regex) {
            foreach ($statements as $statement) {
                $tokens[] = /* ... */;
            }
        }

        return $tokens;
    }
}

class Lexer
{
    public function lexify(array $tokens): array
    {
        $ast = [];
        foreach ($tokens as $token) {
            $ast[] = /* ... */;
        }

        return $ast;
    }
}

class BetterJSAlternative
{
    private $tokenizer;
    private $lexer;

    public function __construct(Tokenizer $tokenizer, Lexer $lexer)
    {
        $this->tokenizer = $tokenizer;
        $this->lexer = $lexer;
    }

    public function parse(string $code): void
    {
        $tokens = $this->tokenizer->tokenize($code);
        $ast = $this->lexer->lexify($tokens);
        foreach ($ast as $node) {
            // parse...
        }
    }
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از flag به عنوان پارامتر در تابع استفاده نکنید

فلگ‌ها به کارب این پیغام را می‌رسانند که این تابع بیش از یک کار انجام می‌دهد. توابع
باید یک کار انجام دهند. اگر توابع شما مسیرهای مختلفی را بر اساس یک متغیر بولی طی
می‌کنند، باید شکسته شوند.

**بد:**

```php
function createFile(string $name, bool $temp = false): void
{
    if ($temp) {
        touch('./temp/'.$name);
    } else {
        touch($name);
    }
}
```

**خوب:**

```php
function createFile(string $name): void
{
    touch($name);
}

function createTempFile(string $name): void
{
    touch('./temp/'.$name);
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از تاثیرات جانبی دوری کنید

یک تابع دارای اثر جانبی است اگر هر کاری به غیر از دریافت ورودی و برگرداندن مقدار یا
مقادیر دیگری انجام دهد. اثر جانبی می‌تواند نوشتن روی یک فایل، تغییر دادن یک متغیر
جهانی یا به طور اتفاقی انتقال تمام پول شما به یک غریبه باشد.

مواردی است که نیاز دارید که در برنامه خود اثر جانبی داشته باشید. مثل مثلا قبلی، احتمال
دارد نیاز داشته باشید در یک فایل بنویسید. کاری که باید انجام دهید این است که جایی که
این کار را انجام می‌دهید را در یک نقطه متمرکز کنید. تعداد زیادی تابع و کلاس که روی فایل
خاصی می‌نویسند نداشته باشید. یک سرویس ایجاد کنید که این کار را انجام دهد. یکی و فقط یکی.

نکته اصلی این است که از تله‌های رایج مانند اشتراک گذاری حالت بین دو شیء بدون هیچ ساختاری،
استفاده از نوع داده‌های تغییر پذیر که می‌توان در آنها هر چیزی نوشت، و مجتمع نکردن جایی که
اثرات جانبی شما بوجود می‌آیند دوری کنید. اگر این کار را بکنید، از اکثریت برنامه نویسان
دیگر شادتر خواهید بود.

**بد:**

```php
// تابع زیر از متغیر جهانی استفاده کرده.
// اگر تابع دیگری داشتیم که از این متغیر استفاده کرده بود، الان این متغیر حاوی یک آرایه
// است و ممکن است آن تابع را خراب کند.
$name = 'Ryan McDermott';

function splitIntoFirstAndLastName(): void
{
    global $name;

    $name = explode(' ', $name);
}

splitIntoFirstAndLastName();

var_dump($name); // ['Ryan', 'McDermott'];
```

**خوب:**

```php
function splitIntoFirstAndLastName(string $name): array
{
    return explode(' ', $name);
}

$name = 'Ryan McDermott';
$newName = splitIntoFirstAndLastName($name);

var_dump($name); // 'Ryan McDermott';
var_dump($newName); // ['Ryan', 'McDermott'];
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### در توابع جانی چیزی ننویسید

تغییر دادن گلوبال‌ها رد بیشتر زبان‌ها مشکل ساز است. زیرا می‌تواند با یک کتابخانه دیگر
تداخل داشته باشد و کاربر API شما متوجه موضوع نشود تا زمانی که در زمان اجرا با اکسپشن
روبرو شود. به این مثال توجه کنید: چی میشه اگر بخواهید یک آرایه پیکربندی داشته باشید؟
می‌توانید یک تابع جهانی مانند `config()` بنویسید، ولی این کار می‌تواند تداخلی با یک
کتابخانه دیگر که میخواهد دقیقا همین کار را انجام دهد داشته باشد.

**بد:**

```php
function config(): array
{
    return  [
        'foo' => 'bar',
    ]
}
```

**خوب:**

```php
class Configuration
{
    private $configuration = [];

    public function __construct(array $configuration)
    {
        $this->configuration = $configuration;
    }

    public function get(string $key): ?string
    {
        return isset($this->configuration[$key]) ? $this->configuration[$key] : null;
    }
}
```

بارگذاری تنظیمات و ایجاد یک نمونه از کلاس `Configuration`

```php
$configuration = new Configuration([
    'foo' => 'bar',
]);
```

و شما باید این نمونه از `Configuration` را در اپلیکیشن خود استفاده کنید.

**[⬆ بازگشت به بالا](#table-of-contents)**

### از الگوی Singleton استفاده نکنید

سینگلتون یک [ضد الگو](https://en.wikipedia.org/wiki/Singleton_pattern) است. توسط Brian Button تفسیر شده:
 1. آنها معمولا به عنوان یک **نمونه جهانی** استفاده می‌شوند، چرا این خیلی بد است؟ چون **شما وابستگی‌های برنامه را در کد پنهان می‌کنید**، در صورتی که باید از طریق اینترفیس آنها را افشا کنید. گلوبال کردن چیزها برای اجتناب از پاس کردن آنها [بوی کد](https://en.wikipedia.org/wiki/Code_smell) است.
 2. آنها [اصل مسئولیت واحد](#single-responsibility-principle-srp) را نقض می‌کنند: با توجه به این واقعیت که **آنها ایجاد و چرخه حیات خود را کنترل می‌کنند**.
 3. آنها ذاتا کد را به شدت [در هم تنیده](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29) می‌کنند. این باعث می‌شود در بسیاری از موارد در زمره کدهای **با تست بسیار سخت** قرار گیرند.
 4. آنها state را در چرخه زندگی نرم افزار با خود حمل می‌کنند. که ضربه بزرگی به تست است. از آنجا که **می‌تواند شما را در وضعیتی قرار دهد که تست‌ها لازم باشد ترتیب داشته باشند** که مانع بزرگی برای unit testها است. چرا؟ چون هر یونیت تست باید مستقل از دیگری باشد.

همچنین نظرات بسیاری خوبی از [Misko Hevery](http://misko.hevery.com/about/) درباره [ریشه مشکل](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/) وجود دارد.

**بد:**

```php
class DBConnection
{
    private static $instance;

    private function __construct(string $dsn)
    {
        // ...
    }

    public static function getInstance(): DBConnection
    {
        if (self::$instance === null) {
            self::$instance = new self();
        }

        return self::$instance;
    }

    // ...
}

$singleton = DBConnection::getInstance();
```

**خوب:**

```php
class DBConnection
{
    public function __construct(string $dsn)
    {
        // ...
    }

     // ...
}
```

نمونه‌ای از کلاس `DBConnection` درست کرده و توسط [DSN](http://php.net/manual/en/pdo.construct.php#refsect1-pdo.construct-parameters) تنظیمات را انجام دهید.

```php
$connection = new DBConnection($dsn);
```

الان باید نمونه `DBConnection` را در برنامه خود استفاده کنید.

**[⬆ بازگشت به بالا](#table-of-contents)**

### عبارات شرطی را کپسوله سازی کنید

**بد:**

```php
if ($article->state === 'published') {
    // ...
}
```

**خوب:**

```php
if ($article->isPublished()) {
    // ...
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از عبارات شرطی منفی دوری کنید

**بد:**

```php
function isDOMNodeNotPresent(\DOMNode $node): bool
{
    // ...
}

if (!isDOMNodeNotPresent($node))
{
    // ...
}
```

**خوب:**

```php
function isDOMNodePresent(\DOMNode $node): bool
{
    // ...
}

if (isDOMNodePresent($node)) {
    // ...
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از عبارات شرطی دوری کنید

این یکی غیر ممکن به نظر میرسه. اولین باری که بیشتر افراد این را میشنوند، می‌گویند،
«چجوری باید بدون استفاده از `if` اصلا کاری بکنم؟» جواب این است که می‌توانید در اکثر موارد
از پلی مورفیسم برای رسیدن به همان نتیجه استفاده کنید. معمولا سوال دوم این است که، «این
خیلی خوبه ولی چرا باید این کارو بکنم؟» جواب در یک مفهوم کد تمیز دیگر است که قبلا خواندیم:
هر تابع فقط باید یک کار انجام دهد. وقتی شما کلاس‌ها و توابعی دارید که از شرط‌های `if` استفاده
می‌کنند، به کاربر می‌گویید که تابع شما بیش از یک کار انجام می‌دهد. به یاد داشته باشید،
فقط یک کار انجام دهید.

**بد:**

```php
class Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        switch ($this->type) {
            case '777':
                return $this->getMaxAltitude() - $this->getPassengerCount();
            case 'Air Force One':
                return $this->getMaxAltitude();
            case 'Cessna':
                return $this->getMaxAltitude() - $this->getFuelExpenditure();
        }
    }
}
```

**خوب:**

```php
interface Airplane
{
    // ...

    public function getCruisingAltitude(): int;
}

class Boeing777 implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getPassengerCount();
    }
}

class AirForceOne implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude();
    }
}

class Cessna implements Airplane
{
    // ...

    public function getCruisingAltitude(): int
    {
        return $this->getMaxAltitude() - $this->getFuelExpenditure();
    }
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از چک کردن نوع دوری کنید (بخش ۱)

PHP یک زبان برنامه نویسی که در آن نوع داده تعریف نمی‌شود، بدین معنی که تابع شما می‌تواند
هر نوع پارامتری بگیرد. در برخی موارد این آزادی شما را وسوسه می‌کند تا نوع داده را در تابع
خود چک کنید. راه‌های مختلفی برای جلوگیری از انجام این کار وجود دارد. اولین چیزی که باید
در نظر داشته باشید API‌های ثابت است.

**بد:**

```php
function travelToTexas($vehicle): void
{
    if ($vehicle instanceof Bicycle) {
        $vehicle->pedalTo(new Location('texas'));
    } elseif ($vehicle instanceof Car) {
        $vehicle->driveTo(new Location('texas'));
    }
}
```

**خوب:**

```php
function travelToTexas(Vehicle $vehicle): void
{
    $vehicle->travelTo(new Location('texas'));
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### از چک کردن نوع دوری کنید (بخش ۲)

اگر با نوع داده‌های ساده اولیه مانند رشته‌ها، اعداد صحیح و آرایه‌ها استفاده می‌کنید و
همچنین از PHP 7+ استفاده می‌کنید و نمیتوانید از پلی مورفیسم سود ببرید اما هنوز نیاز
به چک کردن نوع داده را حس می‌کنید، باید [اعلان نوع](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration)
یا حالد سخت گیرانه را در نظر بگیرید. این کار امکان اعمال نوع داده استاتیک روی سینتاکس
استاندارد PHP را به شما می‌دهد. مشکل چک کردن نوع به صورت دستی این است که انجام این کار
نیاز به دراز گویی فراوان دارد که «امنیت نوع داده» ای که به دست می‌آورید خوانایی از دست
رفته را جبران نمی‌کند. کد PHP خود را تمیز نگهدارید، تست‌های خوب بنویسید، و مرور کدهای خوبی
انجام دهید. دی غیر اینصورت، همه این کارها را انجام دهید ولی با تعریف نوع داده سختگیرانه
در PHP یا حالت سخت گیرانه.

**بد:**

```php
function combine($val1, $val2): int
{
    if (!is_numeric($val1) || !is_numeric($val2)) {
        throw new \Exception('Must be of type Number');
    }

    return $val1 + $val2;
}
```

**خوب:**

```php
function combine(int $val1, int $val2): int
{
    return $val1 + $val2;
}
```

**[⬆ بازگشت به بالا](#table-of-contents)**

### کد مرده را حذف کنید

کد مرده به بدی کد تکراری است. هیچ دلیلی برای نگهداری آن در کدهایتان وجود ندارد. اگر
آن را در هیچ جای برنامه صدا نزده‌اید، از شرش خلاص شوید! اگر باز هم به آن کد نیاز داشتید
در تاریخچه سیستم کنترل ورژن شما وجود دارد.

**بد:**

```php
function oldRequestModule(string $url): void
{
    // ...
}

function newRequestModule(string $url): void
{
    // ...
}

$request = newRequestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**خوب:**

```php
function requestModule(string $url): void
{
    // ...
}

$request = requestModule($requestUrl);
inventoryTracker('apples', $request, 'www.inventory-awesome.io');
```

**[⬆ بازگشت به بالا](#table-of-contents)**


## اشیا و ساختمان داده

### از کپسوله سازی شیء استفاده کنید

در PHP امکان تنظیم کلمات کلیدی `public`، `protected` و `private` برای متدها وجود دارد.
با استفاده از این قابلیت، می‌توانید تغییرات خواص شیء را کنترل کنید.

* وقتی می‌خواهید کاری بیشتر از گرفتم یک خاصیت از شیء را انجام دهید،‌ لازم نیست که بگردید
و هر دسترسی در کد شما وجود دارد را تغییر دهید.
* اعتبار سنجی را وقتی بر روی یک `set` کار می‌کنید راحت تر می‌کند.
* اراه داخلی را کپسوله می کند.
* افزودن گزارش گیری و مدیریت خطالها در هنگام گرفتن و تنظیم ساده‌تر خواهد بود.
* با ارث بری از این کلاس، می‌توانید کارایی آن را بازنویسی کنید.
* می‌توانید خواص شیء خود را در حالت تنبل بارگذاری کنید، بگذارید بگویم آنها را از سرور
بگیرید.

به علاوه این بخشی از اصل [Open/Closed](#openclosed-principle-ocp) است.

**بد:**

```php
class BankAccount
{
    public $balance = 1000;
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->balance -= 100;
```

**خوب:**

```php
class BankAccount
{
    private $balance;

    public function __construct(int $balance = 1000)
    {
      $this->balance = $balance;
    }

    public function withdraw(int $amount): void
    {
        if ($amount > $this->balance) {
            throw new \Exception('Amount greater than available balance.');
        }

        $this->balance -= $amount;
    }

    public function deposit(int $amount): void
    {
        $this->balance += $amount;
    }

    public function getBalance(): int
    {
        return $this->balance;
    }
}

$bankAccount = new BankAccount();

// Buy shoes...
$bankAccount->withdraw($shoesPrice);

// Get balance
$balance = $bankAccount->getBalance();
```

**[⬆ back to top](#table-of-contents)**

### کاری کنید که اشیاء اعضای private/protected داشته باشند

* خواص و متدهای `public` برای تغییرات خطرناک‌ترین‌ها هستند، زیرا یک کد خارجی ممکن است به سادگی به آنها تکیه کند و نمی‌توانید کنترل کنید که چه کدی به آنها وابسته است. **تغییر دادن در کلاس برای همه کاربران آن کلاس خطرناک است.**
* اصلاح کننده `protected` هم مانند `public` خطرناک است، زیرا در اسکوپ هر کلاس فرزند در دسترس هستند. این بدان معناست که تفاوت بین public و protected فقط در مکانیسم دسترسی است، ولی پشتیبانی از کپسوله سازی به همان شکل قبل باقی می‌ماند. **تغییر دادن در کلاس بریا همه فرزندان کلاس خطرناک است**
* اصلاح کننده `private` گارانتی می‌کند که **تغییر کد فقط در مرز همان کلاس خطرناک است.** (شما در تغییرات امنیت دارید و عارضه [اثر Jenga](http://www.urbandictionary.com/define.php?term=Jengaphobia&defid=2494196) را نخواهید داشت).

به همید دلیل به صورت پیش فرض از `private` استفاده کنید و از `public/protected` زمانی استفاده کنید که نیاز به ارائه دسترسی توسط کلاس‌های خارجی دارید.

برای اطلاعات بیشتر این [پست وبلاگ](http://fabien.potencier.org/pragmatism-over-theory-protected-vs-private.html) درباره همین موضوع که توسط [Fabien Potencier](https://github.com/fabpot) نوشته شده را مطالعه کنید.

**بد:**

```php
class Employee
{
    public $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->name; // Employee name: John Doe
```

**خوب:**

```php
class Employee
{
    private $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    public function getName(): string
    {
        return $this->name;
    }
}

$employee = new Employee('John Doe');
echo 'Employee name: '.$employee->getName(); // Employee name: John Doe
```

**[⬆ back to top](#table-of-contents)**

## Classes

### Prefer composition over inheritance

As stated famously in [*Design Patterns*](https://en.wikipedia.org/wiki/Design_Patterns) by the Gang of Four,
you should prefer composition over inheritance where you can. There are lots of
good reasons to use inheritance and lots of good reasons to use composition.
The main point for this maxim is that if your mind instinctively goes for
inheritance, try to think if composition could model your problem better. In some
cases it can.

You might be wondering then, "when should I use inheritance?" It
depends on your problem at hand, but this is a decent list of when inheritance
makes more sense than composition:

1. Your inheritance represents an "is-a" relationship and not a "has-a"
relationship (Human->Animal vs. User->UserDetails).
2. You can reuse code from the base classes (Humans can move like all animals).
3. You want to make global changes to derived classes by changing a base class.
(Change the caloric expenditure of all animals when they move).

**Bad:**

```php
class Employee
{
    private $name;
    private $email;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    // ...
}

// Bad because Employees "have" tax data.
// EmployeeTaxData is not a type of Employee

class EmployeeTaxData extends Employee
{
    private $ssn;
    private $salary;

    public function __construct(string $name, string $email, string $ssn, string $salary)
    {
        parent::__construct($name, $email);

        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}
```

**Good:**

```php
class EmployeeTaxData
{
    private $ssn;
    private $salary;

    public function __construct(string $ssn, string $salary)
    {
        $this->ssn = $ssn;
        $this->salary = $salary;
    }

    // ...
}

class Employee
{
    private $name;
    private $email;
    private $taxData;

    public function __construct(string $name, string $email)
    {
        $this->name = $name;
        $this->email = $email;
    }

    public function setTaxData(string $ssn, string $salary)
    {
        $this->taxData = new EmployeeTaxData($ssn, $salary);
    }

    // ...
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid fluent interfaces

A [Fluent interface](https://en.wikipedia.org/wiki/Fluent_interface) is an object
oriented API that aims to improve the readability of the source code by using
[Method chaining](https://en.wikipedia.org/wiki/Method_chaining).

While there can be some contexts, frequently builder objects, where this
pattern reduces the verbosity of the code (for example the [PHPUnit Mock Builder](https://phpunit.de/manual/current/en/test-doubles.html)
or the [Doctrine Query Builder](http://docs.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/query-builder.html)),
more often it comes at some costs:

1. Breaks [Encapsulation](https://en.wikipedia.org/wiki/Encapsulation_%28object-oriented_programming%29).
2. Breaks [Decorators](https://en.wikipedia.org/wiki/Decorator_pattern).
3. Is harder to [mock](https://en.wikipedia.org/wiki/Mock_object) in a test suite.
4. Makes diffs of commits harder to read.

For more informations you can read the full [blog post](https://ocramius.github.io/blog/fluent-interfaces-are-evil/)
on this topic written by [Marco Pivetta](https://github.com/Ocramius).

**Bad:**

```php
class Car
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake(string $make): self
    {
        $this->make = $make;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function setModel(string $model): self
    {
        $this->model = $model;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function setColor(string $color): self
    {
        $this->color = $color;

        // NOTE: Returning this for chaining
        return $this;
    }

    public function dump(): void
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = (new Car())
  ->setColor('pink')
  ->setMake('Ford')
  ->setModel('F-150')
  ->dump();
```

**Good:**

```php
class Car
{
    private $make = 'Honda';
    private $model = 'Accord';
    private $color = 'white';

    public function setMake(string $make): void
    {
        $this->make = $make;
    }

    public function setModel(string $model): void
    {
        $this->model = $model;
    }

    public function setColor(string $color): void
    {
        $this->color = $color;
    }

    public function dump(): void
    {
        var_dump($this->make, $this->model, $this->color);
    }
}

$car = new Car();
$car->setColor('pink');
$car->setMake('Ford');
$car->setModel('F-150');
$car->dump();
```

**[⬆ back to top](#table-of-contents)**

### Prefer final classes

The `final` should be used whenever possible:

1. It prevents uncontrolled inheritance chain.
2. It encourages [composition](#prefer-composition-over-inheritance).
3. It encourages the [Single Responsibility Pattern](#single-responsibility-principle-srp).
4. It encourages developers to use your public methods instead of extending the class to get access on protected ones.
5. It allows you to change your code without any break of applications that use your class.

The only condition is that your class should implement an interface and no other public methods are defined.

For more informations you can read [the blog post](https://ocramius.github.io/blog/when-to-declare-classes-final/) on this topic written by [Marco Pivetta (Ocramius)](https://ocramius.github.io/).

**Bad:**

```php
final class Car
{
    private $color;

    public function __construct($color)
    {
        $this->color = $color;
    }

    /**
     * @return string The color of the vehicle
     */
    public function getColor()
    {
        return $this->color;
    }
}
```

**Good:**

```php
interface Vehicle
{
    /**
     * @return string The color of the vehicle
     */
    public function getColor();
}

final class Car implements Vehicle
{
    private $color;

    public function __construct($color)
    {
        $this->color = $color;
    }

    /**
     * {@inheritdoc}
     */
    public function getColor()
    {
        return $this->color;
    }
}
```

**[⬆ back to top](#table-of-contents)**

## SOLID

**SOLID** is the mnemonic acronym introduced by Michael Feathers for the first five principles named by Robert Martin, which meant five basic principles of object-oriented programming and design.

 * [S: Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
 * [O: Open/Closed Principle (OCP)](#openclosed-principle-ocp)
 * [L: Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
 * [I: Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
 * [D: Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)

### Single Responsibility Principle (SRP)

As stated in Clean Code, "There should never be more than one reason for a class
to change". It's tempting to jam-pack a class with a lot of functionality, like
when you can only take one suitcase on your flight. The issue with this is
that your class won't be conceptually cohesive and it will give it many reasons
to change. Minimizing the amount of times you need to change a class is important.
It's important because if too much functionality is in one class and you modify a piece of it,
it can be difficult to understand how that will affect other dependent modules in
your codebase.

**Bad:**

```php
class UserSettings
{
    private $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }

    public function changeSettings(array $settings): void
    {
        if ($this->verifyCredentials()) {
            // ...
        }
    }

    private function verifyCredentials(): bool
    {
        // ...
    }
}
```

**Good:**

```php
class UserAuth
{
    private $user;

    public function __construct(User $user)
    {
        $this->user = $user;
    }

    public function verifyCredentials(): bool
    {
        // ...
    }
}

class UserSettings
{
    private $user;
    private $auth;

    public function __construct(User $user)
    {
        $this->user = $user;
        $this->auth = new UserAuth($user);
    }

    public function changeSettings(array $settings): void
    {
        if ($this->auth->verifyCredentials()) {
            // ...
        }
    }
}
```

**[⬆ back to top](#table-of-contents)**

### Open/Closed Principle (OCP)

As stated by Bertrand Meyer, "software entities (classes, modules, functions,
etc.) should be open for extension, but closed for modification." What does that
mean though? This principle basically states that you should allow users to
add new functionalities without changing existing code.

**Bad:**

```php
abstract class Adapter
{
    protected $name;

    public function getName(): string
    {
        return $this->name;
    }
}

class AjaxAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'ajaxAdapter';
    }
}

class NodeAdapter extends Adapter
{
    public function __construct()
    {
        parent::__construct();

        $this->name = 'nodeAdapter';
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch(string $url): Promise
    {
        $adapterName = $this->adapter->getName();

        if ($adapterName === 'ajaxAdapter') {
            return $this->makeAjaxCall($url);
        } elseif ($adapterName === 'httpNodeAdapter') {
            return $this->makeHttpCall($url);
        }
    }

    private function makeAjaxCall(string $url): Promise
    {
        // request and return promise
    }

    private function makeHttpCall(string $url): Promise
    {
        // request and return promise
    }
}
```

**Good:**

```php
interface Adapter
{
    public function request(string $url): Promise;
}

class AjaxAdapter implements Adapter
{
    public function request(string $url): Promise
    {
        // request and return promise
    }
}

class NodeAdapter implements Adapter
{
    public function request(string $url): Promise
    {
        // request and return promise
    }
}

class HttpRequester
{
    private $adapter;

    public function __construct(Adapter $adapter)
    {
        $this->adapter = $adapter;
    }

    public function fetch(string $url): Promise
    {
        return $this->adapter->request($url);
    }
}
```

**[⬆ back to top](#table-of-contents)**

### Liskov Substitution Principle (LSP)

This is a scary term for a very simple concept. It's formally defined as "If S
is a subtype of T, then objects of type T may be replaced with objects of type S
(i.e., objects of type S may substitute objects of type T) without altering any
of the desirable properties of that program (correctness, task performed,
etc.)." That's an even scarier definition.

The best explanation for this is if you have a parent class and a child class,
then the base class and child class can be used interchangeably without getting
incorrect results. This might still be confusing, so let's take a look at the
classic Square-Rectangle example. Mathematically, a square is a rectangle, but
if you model it using the "is-a" relationship via inheritance, you quickly
get into trouble.

**Bad:**

```php
class Rectangle
{
    protected $width = 0;
    protected $height = 0;

    public function setWidth(int $width): void
    {
        $this->width = $width;
    }

    public function setHeight(int $height): void
    {
        $this->height = $height;
    }

    public function getArea(): int
    {
        return $this->width * $this->height;
    }
}

class Square extends Rectangle
{
    public function setWidth(int $width): void
    {
        $this->width = $this->height = $width;
    }

    public function setHeight(int $height): void
    {
        $this->width = $this->height = $height;
    }
}

function printArea(Rectangle $rectangle): void
{
    $rectangle->setWidth(4);
    $rectangle->setHeight(5);

    // BAD: Will return 25 for Square. Should be 20.
    echo sprintf('%s has area %d.', get_class($rectangle), $rectangle->getArea()).PHP_EOL;
}

$rectangles = [new Rectangle(), new Square()];

foreach ($rectangles as $rectangle) {
    printArea($rectangle);
}
```

**Good:**

The best way is separate the quadrangles and allocation of a more general subtype for both shapes.

Despite the apparent similarity of the square and the rectangle, they are different.
A square has much in common with a rhombus, and a rectangle with a parallelogram, but they are not subtype.
A square, a rectangle, a rhombus and a parallelogram are separate shapes with their own properties, albeit similar.

```php
interface Shape
{
    public function getArea(): int;
}

class Rectangle implements Shape
{
    private $width = 0;
    private $height = 0;

    public function __construct(int $width, int $height)
    {
        $this->width = $width;
        $this->height = $height;
    }

    public function getArea(): int
    {
        return $this->width * $this->height;
    }
}

class Square implements Shape
{
    private $length = 0;

    public function __construct(int $length)
    {
        $this->length = $length;
    }

    public function getArea(): int
    {
        return $this->length ** 2;
    }
}

function printArea(Shape $shape): void
{
    echo sprintf('%s has area %d.', get_class($shape), $shape->getArea()).PHP_EOL;
}

$shapes = [new Rectangle(4, 5), new Square(5)];

foreach ($shapes as $shape) {
    printArea($shape);
}
```

**[⬆ back to top](#table-of-contents)**

### Interface Segregation Principle (ISP)

ISP states that "Clients should not be forced to depend upon interfaces that
they do not use."

A good example to look at that demonstrates this principle is for
classes that require large settings objects. Not requiring clients to set up
huge amounts of options is beneficial, because most of the time they won't need
all of the settings. Making them optional helps prevent having a "fat interface".

**Bad:**

```php
interface Employee
{
    public function work(): void;

    public function eat(): void;
}

class HumanEmployee implements Employee
{
    public function work(): void
    {
        // ....working
    }

    public function eat(): void
    {
        // ...... eating in lunch break
    }
}

class RobotEmployee implements Employee
{
    public function work(): void
    {
        //.... working much more
    }

    public function eat(): void
    {
        //.... robot can't eat, but it must implement this method
    }
}
```

**Good:**

Not every worker is an employee, but every employee is a worker.

```php
interface Workable
{
    public function work(): void;
}

interface Feedable
{
    public function eat(): void;
}

interface Employee extends Feedable, Workable
{
}

class HumanEmployee implements Employee
{
    public function work(): void
    {
        // ....working
    }

    public function eat(): void
    {
        //.... eating in lunch break
    }
}

// robot can only work
class RobotEmployee implements Workable
{
    public function work(): void
    {
        // ....working
    }
}
```

**[⬆ back to top](#table-of-contents)**

### Dependency Inversion Principle (DIP)

This principle states two essential things:
1. High-level modules should not depend on low-level modules. Both should
depend on abstractions.
2. Abstractions should not depend upon details. Details should depend on
abstractions.

This can be hard to understand at first, but if you've worked with PHP frameworks (like Symfony), you've seen an implementation of this principle in the form of Dependency
Injection (DI). While they are not identical concepts, DIP keeps high-level
modules from knowing the details of its low-level modules and setting them up.
It can accomplish this through DI. A huge benefit of this is that it reduces
the coupling between modules. Coupling is a very bad development pattern because
it makes your code hard to refactor.

**Bad:**

```php
class Employee
{
    public function work(): void
    {
        // ....working
    }
}

class Robot extends Employee
{
    public function work(): void
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage(): void
    {
        $this->employee->work();
    }
}
```

**Good:**

```php
interface Employee
{
    public function work(): void;
}

class Human implements Employee
{
    public function work(): void
    {
        // ....working
    }
}

class Robot implements Employee
{
    public function work(): void
    {
        //.... working much more
    }
}

class Manager
{
    private $employee;

    public function __construct(Employee $employee)
    {
        $this->employee = $employee;
    }

    public function manage(): void
    {
        $this->employee->work();
    }
}
```

**[⬆ back to top](#table-of-contents)**

## Don’t repeat yourself (DRY)

Try to observe the [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) principle.

Do your absolute best to avoid duplicate code. Duplicate code is bad because
it means that there's more than one place to alter something if you need to
change some logic.

Imagine if you run a restaurant and you keep track of your inventory: all your
tomatoes, onions, garlic, spices, etc. If you have multiple lists that
you keep this on, then all have to be updated when you serve a dish with
tomatoes in them. If you only have one list, there's only one place to update!

Often you have duplicate code because you have two or more slightly
different things, that share a lot in common, but their differences force you
to have two or more separate functions that do much of the same things. Removing
duplicate code means creating an abstraction that can handle this set of different
things with just one function/module/class.

Getting the abstraction right is critical, that's why you should follow the
SOLID principles laid out in the [Classes](#classes) section. Bad abstractions can be
worse than duplicate code, so be careful! Having said this, if you can make
a good abstraction, do it! Don't repeat yourself, otherwise you'll find yourself
updating multiple places any time you want to change one thing.

**Bad:**

```php
function showDeveloperList(array $developers): void
{
    foreach ($developers as $developer) {
        $expectedSalary = $developer->calculateExpectedSalary();
        $experience = $developer->getExperience();
        $githubLink = $developer->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}

function showManagerList(array $managers): void
{
    foreach ($managers as $manager) {
        $expectedSalary = $manager->calculateExpectedSalary();
        $experience = $manager->getExperience();
        $githubLink = $manager->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Good:**

```php
function showList(array $employees): void
{
    foreach ($employees as $employee) {
        $expectedSalary = $employee->calculateExpectedSalary();
        $experience = $employee->getExperience();
        $githubLink = $employee->getGithubLink();
        $data = [
            $expectedSalary,
            $experience,
            $githubLink
        ];

        render($data);
    }
}
```

**Very good:**

It is better to use a compact version of the code.

```php
function showList(array $employees): void
{
    foreach ($employees as $employee) {
        render([
            $employee->calculateExpectedSalary(),
            $employee->getExperience(),
            $employee->getGithubLink()
        ]);
    }
}
```

**[⬆ back to top](#table-of-contents)**

## Translations

This is also available in other languages:

* :cn: **Chinese:**
   * [php-cpm/clean-code-php](https://github.com/php-cpm/clean-code-php)
* :ru: **Russian:**
   * [peter-gribanov/clean-code-php](https://github.com/peter-gribanov/clean-code-php)
* :es: **Spanish:**
   * [fikoborquez/clean-code-php](https://github.com/fikoborquez/clean-code-php)
* :brazil: **Portuguese:**
   * [fabioars/clean-code-php](https://github.com/fabioars/clean-code-php)
   * [jeanjar/clean-code-php](https://github.com/jeanjar/clean-code-php/tree/pt-br)
* :thailand: **Thai:**
   * [panuwizzle/clean-code-php](https://github.com/panuwizzle/clean-code-php)
* :fr: **French:**
   * [errorname/clean-code-php](https://github.com/errorname/clean-code-php)
* :vietnam: **Vietnamese**
   * [viethuongdev/clean-code-php](https://github.com/viethuongdev/clean-code-php)
* :kr: **Korean:**
   * [yujineeee/clean-code-php](https://github.com/yujineeee/clean-code-php)
* :tr: **Turkish:**
   * [anilozmen/clean-code-php](https://github.com/anilozmen/clean-code-php)

**[⬆ back to top](#table-of-contents)**
