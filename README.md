# Kotlin Code Style Guide

## Содержание

1. [Наименование](#Наименование)
    - [Пакеты](#Пакеты)
    - [Типы](#Типы)
        - [Классы](#Классы)
        - [Базовые классы](#Базовые-классы)
        - [Абстрактные классы](#Абстрактные-классы)
        - [Интерфейсы](#Интерфейсы)
        - [Классы, эксклюзивно реализующие интерфейс](#Классы-эксклюзивно-реализующие-интерфейс)
        - [Типы-перечисления](#Типы-перечисления)
    - [Свойства](#Свойства)
        - [Константы](#Константы)
    - [Функции](#Функции)
        - [Функции, возвращающие `Boolean`](#Функции-возвращающие-boolean)
        - [Функции обратного вызова](#Функции-обратного-вызова)
2. [Объявления на уровне файла](#Объявления-на-уровне-файла)
    - [Объявление констант](#Объявление-констант)
3. [Структура класса](#Структура-класса)
    - [Порядок функций и свойств](#Порядок-функций-и-свойств)
4. [Форматирование](#Форматирование)
    - [Ограничение длины строки](#Ограничение-длины-строки)
        - [Правила переносов](#Правила-переносов)
    - [Форматирование заголовка класса](#Форматирование-заголовка-класса)
    - [Форматирование функций](#Форматирование-функций)
        - [Сигнатура функции](#Сигнатура-функции)
        - [Вызов функции](#Вызов-функции)
        - [Именованные аргументы](#Именованные-аргументы)
        - [Функциональные типы](#Функциональные-типы)
        - [Тело функции](#Тело-функции)
        - [Пояснительные переменные в функциях](#Пояснительные-переменные-в-функциях )
        - [Размер функции](#Размер-функции)
        - [Функции-выражения](#Функции-выражения)
    - [Ссылки на функции](#Ссылки-на-функции)
        - [Ссылки на свойства](#Ссылки-на-свойства)
    - [Цепочки вызовов](#Цепочки-вызовов)
    - [Переопределение `set` и `get`](#Переопределение-set-и-get)
    - [Аннотации](#Аннотации)
        - [Аннотации типов](#Аннотации-типов)
        - [Аннотации функций](#Аннотации-функций)
        - [Аннотации свойств](#Аннотации-свойств)
    - [Блоки управления](#Блоки-управления)
        - [`if else`](#if-else)
        - [`when`](#when)
        - [`try catch`](#try-catch)
        - [`where`](#where)
    - [Литералы с плавающей запятой](#Литералы-с-плавающей-запятой)
    - [Пустые блоки](#Пустые-блоки)
5. [Идиоматика языка](#Идиоматика-языка)
    - [Замена функции свойством `val`](#Замена-функции-свойством-val)
    - [Презумпция нулевой ссылки](#Презумпция-нулевой-ссылки)
    - [Выход из функции с помощью оператора `?:`](#Выход-из-функции-с-помощью-оператора-elvis)
    - [Аргументы по умолчанию](#Аргументы-по-умолчанию)
6. [Документирование](#Документирование)
    - [KDoc](#kdoc)
    - [Комментарии](#Комментарии)
        - [Форматирование комментариев](#Форматирование-комментариев)
        - [Закомментированный код](#Закомментированный-код)
        - [Комментарии-разделители](#Комментарии-разделители)
        - [Комментарий TODO](#Комментарий-TODO)
7. [Ссылки на источники](#Ссылки-на-источники)


# Наименование

## Пакеты

Имена пакетов набираются в нижнем регистре и не содержат промежуточных разделителей, префиксов
и постфиксов:

```kotlin
su.ati.client.notification.feed  // Ok.
```
```kotlin
su.ati.client.notificationFeed  // Bad: camelCase should be avoided.
```
```kotlin
su.ati.client.notification_feed // Bad: _underscores_ should be avoided.
```

Имена пакетов отражают назначение сгруппированных в них классов, формулируются максимально
коротко, в идеале — одним словом. Если при наименовании пакета появляется потребность в
разделителях, следует по возможности пересмотреть группировку пакетов и/или классов в них.

Пример перегруппировки пакетов по признаку общей функциональности:

```kotlin
su.ati.client.dashboardfeed  --->  su.ati.client.feed.dashboard
su.ati.client.myfeed         --->  su.ati.client.feed.my
su.ati.client.subjectfeed    --->  su.ati.client.feed.subject
```

## Типы

### Классы

Имена классов набираются в PascalCase и могут содержать как существительное (`User`, `Feed`),
так и словосочетание с существительным (`UserCredentials`, `FilteredSearchInput`).
Имя класса сообщает, какую сущность он моделирует, и отражает её назначение (роль).

Общепринятой практикой является именование классов в формате `СущностьРоль`, например:
`ArticleResponseBody`, `ArticlesRepository`, `ProfileFragment`, `SearchViewModel`,
`BookmarkView`, `UserInteractor`, `BlogPostViewHolder`, `CalendarComponent` и т. д.

### Базовые классы

Если необходимо указать, что класс является базовым для всех наследников, то его имя можно
начать с префикса `Base`: `BaseFragment`, `BaseViewModel`, `BaseView`. В сочетании с принципом
`СущностьРоль` имена базовых классов могут приобретать следующий вид:
`BaseFeedAdapter`, `BaseDocumentView` и т. п.

### Абстрактные классы

Допускается использование префиксов `Abs` в именах абстрактных классов, например, `AbsRunner`, `AbsFeedRepository`.
При этом префикс `Base` в имени базовых классов остаётся предпочтительным.

### Интерфейсы

Имена интерфейсов так же набираются в PascalCase, могут содержать существительное, прилагательное
(например, `Editable`) или словосочетание с существительным и/или прилагательным.

**Не рекомендуется** использовать префикс `I` в имени интерфейса (`IRepository`,
`ICallback` и т. п.).

### Классы, эксклюзивно реализующие интерфейс

При следовании принципу отделения интерфейса от реализации в именах классов могут появляться
постфиксы `Impl`. Пример:

```kotlin
interface ArticlesRepository {
    fun getArticles(): Single<List<Article>>
}

class ArticlesRepositoryImpl(private val api: ArticlesApiService) : ArticlesRepository {
    override fun getArticles(): Single<List<Article>> {
        return api.getArticles()
    }
}
```

Такое имя указывает, что данный класс является единственной реализацией данного интерфейса.


### Типы-перечисления

Классы, объявленные с ключевым словом **`enum`**, именуются в PascalCase. Члены данных классов
именуются в верхнем регистре с разделителем `_`. Свойства и функции членов именуются по обычным
правилам, принятым для [свойств](#Свойства) и [функций](#Функции). Примеры:

```kotlin
enum class SortType {
    DATE,
    RELEVANCE,
    IMPORTANCE
}
```

```kotlin
enum class SourceIcon(@DrawableRes val iconResId: Int) {
    EMPTY(R.drawable.ic_search_source_empty),
    ARCHIVE(R.drawable.ic_search_source_archive),
    LOGIC_GROUP(R.drawable.ic_search_source_logic_group);

    companion object {
        fun byIconResId(@DrawableRes iconResId: Int): Icon {
            return values().find { it.iconResId == iconResId } ?: EMPTY
        }
    }

    val hasIcon: Boolean
        get() = this != EMPTY
}
```

В именах членов перечислений **не используются** префиксы, совпадающие с именем самого
перечисления:

```kotlin
enum class State {
    STATE_CONSISTENT,   // Bad.
    STATE_INCONSISTENT  // Bad.
}
```

```kotlin
enum class State {
    CONSISTENT,         // Ok.
    INCONSISTENT        // Ok.
}
```

## Свойства

Свойства именуются в camelCase. Исключением являются "константы", для которых есть
[отдельные правила](#Константы).

```kotlin
var selectedTestAccount: TestAccount? = null
val toolbarDelegate: ToolbarDelegate = ToolbarDelegate()
```

При наименовании свойств **не используются** префиксы-сокращения типов View:
```kotlin
val tvUserName   // Bad.
val tvUserEmail  // Bad.
val ivUserPhoto  // Bad.
```

```kotlin
val userNameTextView    // Ok.
val userEmailTextView   // Ok.
val userPhotoImageView  // Ok.
```

### Константы

К "константам" в языке Kotlin можно условно отнести **глубоко неизменяемые** свойства, не имеющие
переопределённого `get`'ера.

Данные свойства именуются в верхнем регистре с разделителем `_`.

Примеры:

```kotlin
val DEFAULT_SORT_TYPE = SortType.BY_SUBJECT

// Enum type "GuestNavigationTab" has deeply immutable members.
val GUEST_TABS = listOf(
    GuestNavigationTab.LOGIN,
    GuestNavigationTab.CONTACTS,
    GuestNavigationTab.MAKE_APPOINTMENT
)
```

>**Примечание**: глубокая неизменяемость подразумевает, что свойство является _Read-Only_,
а его внутреннее состояние нельзя изменить через публичные члены. Например:
>```kotlin
>val ABC = listOf("A", "B", "C")
>``` 
>Здесь `abc` – _Read-Only_-список неизменяемого типа String. Поскольку внутреннее состояние объекта
String нельзя изменить, такое свойство является глубоко неизменяемым. А вот обратный пример:
>```kotlin
>val midnightCalendar = Calendar.getInstance().setHours(0).setMinutes(0).setSeconds(0)
>```
>Здесь `midnightCalendar` – это _Read-Only_-свойство типа, предоставляющего возможность изменить
>состояние экземпляра в любой момент времени с помощью вызова публичных функций:
>```kotlin
>midnightCalendar.set(Calendar.DAY_OF_MONTH, 1)
>```
>Следовательно, такое свойство не является глубоко неизменяемым.

Свойства примитивного типа или типа `String`, объявленные на уровне файла или в теле **`object`**,
можно превратить в константу времени компиляции, добавив ключевое слово **`const`**.

Примеры:

```kotlin
const val EMPTY_STRING = ""

const val DEFAULT_INDEX = -1

const val ANIMATION_DURATION_MILLIS = 350L

const val REQUEST_CODE_LOGOUT_CONFIRMATION_DIALOG = 10001
```

## Функции

Имя функции отражает действие, которое совершается при её вызове, и выражается глаголом или
словосочетанием с глаголом в инфинитиве: `doSomething()`.

```kotlin
show()

hide()

displayProgress()

buildCells(documents: List<Document>): List<DocumentCell>

setSpinnerItems(items: List<SpinnerItem>, defaultItem: SpinnerItem)
```

Если функция возвращает результат того же типа, на экземпляре которого она вызывается,
то её имя должно сообщать, будет ли создан новый экземпляр, или будет модифицирован исходный.
Например, функции `sort()` и `sortBy()` из `MutableCollections.kt` возвращают исходный экземпляр
коллекции, тогда как функции `sorted()` и `sortedBy()` создают его копию.

Существует несколько особых случаев именования функций, они описаны ниже.

### Функции, возвращающие `Boolean`

Имена `Boolean`-функций, выполняющих исключительно проверку заданного условия, без модификации
аргументов и объекта, на котором они вызываются, могут быть названы вопросительным предложением,
начинающимся с глаголов `is`, `are`, `has`, `contains`, `requires` и т. п.

Классическими примерами здесь служат стандартные функции `Strings.kt` или `Collections.kt`:
`startsWith()`, `isBlank()`, `contains()` и т. д.. Другие примеры:

```kotlin
fun isInputValid(input: String): Boolean {
   return input.isNotBlank() && input.startsWithNumber().not()
}

```

```kotlin
fun areAllCategoriesSelected(
    template: SearchTemplate,
    selectedCategories: List<SearchCategory>
): Boolean {
    val bothOfSameSize = template.categoriesIds.size == selectedCategories.size
    val allCategoriesSelected = template
        .categoriesIds
        .all { id ->
            selectedCategories.any { it.id == id }
        }
    return bothOfSameSize && allCategoriesSelected
}
```

Если `Boolean`-функция не принимает аргументы, то её можно преобразовать в свойство `val`
с переопределённым `get`'ером. Например:

```kotlin
val isInputValid: Boolean
    get() = userNameTextView.isNotBlank() && userNameTextView.isNotBlank()
```

Другие примеры преобразования функций в свойства см. в разделе
[Замена функции свойством `val`](#Замена-функции-свойством-val)

### Функции обратного вызова

Как правило, функции обратного вызова именуются в стиле `onSomethingHappens()`
или `onSomethingHappened()`. К таковым относятся функции интерфейсов-слушателей или абстрактные
функции базовых классов.

Примеры:

```kotlin
interface SubscriptionsStateListener {
    fun onPushSubscriptionStateChange(feedId: Long, isSubscribed: Boolean)
    fun onEmailSubscriptionStateChange(feedId: Long, isSubscribed: Boolean)
}
```

```kotlin
interface CalendarRangeSelectionListener {
    fun onRangeSelected(startRange: Calendar, endRange: Calendar)
}
```

```kotlin
abstract class BaseFragment : Fragment() {

    final override fun onAttach(context: Context) {
        super.onAttach(context)
        
        // Base class function implementation.
        // ...
        
        onAttached(context)
    }

    open fun onAttached(context: Context) = Unit

}
```

# Объявления на уровне файла

Приветствуется объединение близких по смыслу функций и свойств в одном файле.

Например, это может быть набор функций для выполнения похожих действий: `ToastsAndSnacks.kt`,
`Sharing.kt`, `Files.kt`, `Parcellables.kt` и т. п.. Или, к примеру, набор функций расширения,
выполняющих операции с общим типом-получателем: `ContextExtensions.kt`, `ViewExtensions.kt`,
`LiveDataExtensions.kt`, и т. п.

Объединение нескольких публичных типов в одном файле лучше свести к минимуму. Если несколько 
публичных типов объединяются в один файл, то имя этого файла должно хорошо отражать то, что содержится в этом файле. 
В общем случае следует руководствоваться принципом "**Один класс – один файл**".

### Объявление констант

Лучше избегать объявление констант снаружи от тела класса в одном и том же файле.

При размещении констант следует придерживаться следующих рекомендаций:

* Приватные константы следует располагать в **`companion object`** класса.

* Публичные константы, логически связанные с реализацией какого-либо класса (происхождение
  констант и/или их прямое назначение связано с реализацией класса), также следует располагать
  в **`companion object`**'е данного класса.

* Публичные константы, общие для нескольких классов и логически не связанные с реализацией
  какого-либо из них (либо связанные со всеми сразу), могут располагаться во внешнем файле –
  либо в виде объявлений на уровне файла, либо внутри внешнего **`object`**'а.

# Структура класса

Типовой класс имеет следующую разметку:

1. KDoc класса
2. [Заголовок класса](#Форматирование-заголовка-класса)
3. Второстепенные конструкторы класса
4. Объявление внутренних интерфейсов
5. Companion object
6. Типы-перечисления
7. Свойства класса
8. Блок **`init`**
9. Функции класса
10. Объявление внутренних классов

Подобно тому, как статические члены располагаются в самом верху Java-класса, **`companion object`**
располагается в самом верху Kotlin-класса, следуя сразу за объявлениями второстепенных
конструкторов и внутренних интерфейсов.

```kotlin
class NotificationDetailsFragment : Fragment(R.layout.fragment_notification_details) {

    companion object {
        private const val ARGUMENTS = "NotificationDetailsFragment.Arguments"

        fun newInstance(args: NotificationDetailsArgs): Fragment {
            val bundle = bundleOf(ARGUMENTS to args)
            return NotificationDetailsFragment().apply { arguments = bundle }
        }
    }

    private val viewBinding: FragmentNotificationDetailsBinding by viewBinding { view ->
        FragmentNotificationDetailsBinding.bind(view)
    }

    // ...
```

Объявления внутренних классов располагаются в самому низу. Для их визуального отделения можно
пропускать перед ними две строки.

Блок **init** располагается в необходимой точке инициализации класса относительно его свойств –
как правило, перед объявлениями функций.

## Порядок функций и свойств

Каких-то строгих правил по упорядочиванию функций и свойств нет, однако существует несколько
рекомендаций:

### Свойства должны быть логически сгруппированы

Близкие по смыслу и назначению свойства должны находиться рядом – это облегчает их поиск и
даёт подсказку о том, как эти свойства используются. Такие группы отделяются друг от друга и от
отдельно стоящих свойство пустой строкой:

```kotlin
// CalendarDayView.kt

private var drawingRect: RectF = RectF()

private var fillPaint: Paint = Paint(Paint.ANTI_ALIAS_FLAG)
private var fillColor: Int = Color.WHITE

private var strokePaint: Paint = Paint(Paint.ANTI_ALIAS_FLAG)
private var strokeColor: Int = Color.BLACK
```

```kotlin
// NewCommentFragment.kt

val phoneInputView: EditText
val emailInputView: EditText
val commentInputView: EditText

val saveButtonView: AppCompatButton
val cancelButtonView: AppCompatButton

val progressHeaderView: TextView
val progressSubheaderView: TextView
```

Если у класса много свойств, их группы можно задокументировать с помощью обычного комментария
(`//` или `/* */`), либо с помощью разметки `// region <Properties region Name>`. Подробнее см.
в разделе [Комментарии-разделители](#Комментарии-разделители).

### Порядок функций должен быть естественным

Класс читается сверху вниз, поэтому в хорошо структурированном классе вызываемые функции
следуют за вызывающими. Так же как и свойства класса, концептуально родственные функции должны
находиться рядом.

Концептуальное родство может быть основано на выполнении ими взаимосвязанных действий, – когда
несколько функций отвечают за одну часть функциональности класса.

>**Примечание**: полезные рекомендации по упорядочиванию членов класса и форматированию можно
посмотреть в пятой главе книги Роберта С. Мартина "Чистый код" (Robert C. Martin, "Clean Code:
A Handbook of Agile Software Craftsmanship").

**Не следует упорядочивать члены класса по признаку области видимости, наследования или
абстрактности – например, не нужно всегда объявлять private-функции внизу класса, а override –
вверху, если такой порядок не является естественным для данного класса.**

Пример:

```kotlin
class BookmarksController(arguments: Bundle? = null): BaseController(arguments), 
    BookmarksView,
    OnBookmarkRemoveListener {
    
    // Omitted class impl.
    

    // region OnBookmarkRemoveListener impl.
    
    override fun onBookmarkRemoveRequested(bookmarkId: Long) {
        showBookmarkRemoveConfirmationDialog(bookmarkId)
    }

    private fun showBookmarkRemoveConfirmationDialog(bookmarkId: Long) {
        // Opening confirmation dialog here.
    }

    override fun onBookmarkRemoveConfirmed(bookmarkId: Long) {
        // Remove bookmark after successful confirmation.
    }
    
    // endregion

}
```

В данном примере **`private`**-функция `showBookmarkRemoveConfirmationDialog` объявлена следом
за **`override`**-функцией `onBookmarkRemoveRequested`, потому что:

* вызывается из неё
* концептуально связана с остальными функциями реализуемого интерфейса.

### Упорядочивание функций цикла жизни

Существуют практические рекомендации по циклу жизни.

Если класс наследует `Activity`, `Fragment`, `Controller`, `Service` или отражает в себе цикл
жизни таких компонент (например, `ViewModel`, `Presenter`), то следует:

1. Разместить все функции цикла жизни первыми.

2. Упорядочить такие функции по принципу матрёшки:
- [_onStart_ of **Big** lifecycle stage]
    - [_onStart_ of **Medium** lifecycle stage]
        - [_onStart_ of **Small** lifecycle stage]
        - [_onEnd_ of **Small** lifecycle stage]
    - [_onEnd_ of **Medium** lifecycle stage]
- [_onEnd_ of **Big** lifecycle stage]

3. Непарные функции цикла жизни, такие как `onViewCreated()` и `onActivtyCreated()` в `Fragment`,
   разместить в порядке их вызова относительно других функций цикла жизни.

4. Не смешивать их с другими функциями класса.

Для удобства можно выделить данный регион с помощью разметки `// region Lifecycle`.

Данный подход позволяет упростить отслеживание симметрии в работе класса – например,
инициализацию и освобождение ресурсов, а также быстрее обнаружить ошибки, связанные
с циклом жизни.

# Форматирование

## Ограничение длины строки

Длина строки исходного кода ограничена **120 символами**. Весь код, а также KDoc и комментарии,
выходящие за указанный предел, разбиваются на две или более строк.

Исключения:
* Объявления **`package`**
* Директивы **`import`**
* URL в KDoc, комментариях и строковых литералах
* Команды, которые могут быть скопированы из комментариев в терминал

Также исключением могут быть длинные сигнатуры функций без аргументов, правильно разбить которые
на несколько строк не представляется возможным. Например, функции-расширения с параметрами
обобщённых типов:

```kotlin
private fun Observable<MutableList<out BaseDocumentCell>>.applyOpenedMark(): Observable<MutableList<out BaseDocumentCell>> {
    // Function body.
}
```

>**Примечание**: не самым худшим решением будет вообще не проектировать такие функции.

### Правила переносов

> Правила переносов в сигнатурах функций и в заголовках типов см. в разделах
[Форматирование функций](#Форматирование-функций) и
[Форматирование заголовка класса](#Форматирование-заголовка-класса).

> Правила переносов в цепочках вызовов см. в разделе [Цепочки вызовов](#Цепочки-вызовов).

Переносы ставятся

* **после** операторов `=`, `+=`, `-=`, `*=`, `/=`
* **после** операторов `+`, `-`, `*`, `/`
* **после** операторов `>`, `>=`, `<`, `<=`, `==`, `!=`
* **после** операторов `&&` и `||`
* **после** запятой `,`
* **после** открывающей круглой скобки `(`
* **после** стрелки `->` в лямбда-выражении

* **перед** операторами `.`, `?.`, `!!.` и `::`
* **перед** операторами `as`, `as?`, `is`, `!is`
* **перед** оператором elvis `?:`

## Форматирование заголовка класса

Заголовок класса включает:

* Модификаторы, _если присутствуют_
* Ключевое слово **`class`**
* Имя класса
* Параметры обобщённых типов (`<T>`), _если присутствуют_
* Основной (primary) конструктор, _если присутствует_
* Наследуемые типы, _если присутствуют_
* Блок **`where`**, _если присутствует_

Как правило, каждый аргумент основного конструктора выносится на отдельную строку.
Все наследуемые типы выравниваются в одну колонку и при необходимости отделяются одной
пустой строкой:

```kotlin
class ExaminationsListViewModel(
    private val sharingViewModelDelegate: ExaminationSharingViewModelDelegate,
    private val sortablePagedListViewModelDelegate: ExaminationsSortableViewModelDelegate

) : BaseViewModel(),
    SharingObjectViewModel by sharingViewModelDelegate,
    SortablePagedEhrListViewModel by sortablePagedListViewModelDelegate {

    // Class body.
}
```

Аргументы конструктора наследуемого класса так же выравниваются в столбец, а следующие за ними
имена наследуемых интерфейсов отделяются пустой строкой:

```kotlin
// Class header with lots of inheritance.

class ClassWithLotsOfInheritance(
    superClassLong: Long,
    superClassString: String,
    superClassBoolean: Boolean,
    superClassCustomObjectWithLongName: SuperClassCustomObjectWithLongName

) : InheritedClass(
    superClassLong,
    superClassString
), 
    InheritedInterface,
    AnotherInheritedInterface {

    // Class body.
}
```

Весь заголовок класса может располагаться на одной строке, если это не затрудняет его
восприятие, а суммарная длина заголовка не превышает
[лимит символов в строке](#Ограничение-длины-строки).

```kotlin
inline class EhrId(val value: Long)

class Tupple<A, B>(val a: A, val b: B) {
    // Class body.
}

class LoginUseCase(private val gateway: LoginGateway) {
    // Class body.
}

class ShortClassName(superClassArg: Long) : SuperClass(superClassArg) {
    // Class body.
}

class TinyClassName(arg: Int) : SuperClass(arg), SuperInterface, AnotherSuperInterface {
    // Class body.
}
```

### Порядок второстепенных конструкторов

Второстепенные конструкторы объявляются сразу после заголовка класса в "телескопическом" стиле,
то есть в порядке увеличения числа частных аргументов.

```kotlin
class DateModel(val dateInMillis: Long) : Comparable<DateModel> {

    constructor(date: Date) : this(date.time)
    
    constructor(calendar: Calendar) : this(calendar.timeInMillis)
    
    constructor(day: Int, month: Int, year: Int) : this(
        Calendar
            .getInstance()
            .setYear(year)
            .setMonth(month)
            .setDay(day)
            .timeInMillis
    )

    // Class body.
}
```

## Форматирование функций

### Сигнатура функции

Сигнатура функции размещается целиком на одной строке, если:

1. Функция не принимает аргументы.
2. Функция принимает аргументы, и длина её сигнатуры не превышает
   [лимит сиволов в строке](#Ограничение-длины-строки).

Если функция принимает хотя бы один аргумент, и длина её сигнатуры превышает лимит сиволов,
то каждый аргумент функции, а также возвращаемый тип выносятся на отдельную строку:

```kotlin
// SomeCellsAdapter.kt

override fun onCreateCellViewHolder(
    parent: ViewGroup,
    viewType: Int
): BaseCellViewHolder<out AdapterCell> {
    // Function body.
}
```

Колоннообразное форматирование упрощает восприятие функции, поэтому можно считать
его предпочтительным:

```kotlin
// ChangePasswordUseCase.kt

fun buildSingle(
    oldPassword: String,
    newPassword: String
): Single<LoginResultModel> {
    return passwordGateway.confirmPasswordChange(oldPassword, newPassword)
}
```

```kotlin
// LoginApiService.kt

@POST("/auth/login")
fun login(
    @Body body: LoginRequestBody
): Single<Response<LoginResultResponseBody>>

@POST("/auth/refresh")
fun refreshAuth(
    @Body body: RefreshAuthRequestBody
): Single<Response<RefreshAuthResponseBody>>
```

### Вызов функции

Длинные вызовы функций форматируются в виде столбцов:

```kotlin
val motionEvent = MotionEvent.obtain(
    SystemClock.uptimeMillis(),
    SystemClock.uptimeMillis() + durationInMillis,
    MotionEvent.ACTION_DOWN,
    viewSize / 2.0f,
    viewSize / 2.0f,
    0
)
```

Однако аргументы с короткими идентификаторами уместнее перечислять горизонтально:

```kotlin
val week = listOf(day1, day2, day3, day4, day5)
```

>Больше примеров см. в разделе [Цепочки вызовов](#Цепочки-вызовов).

### Именованные аргументы

Именованные аргументы рекомендуется использовать при передаче в функцию каких-либо литералов –
строковых, числовых, булевых или функциональных, так как это упрощает чтение и понимание вызова
функции.

Например, вызов

```kotlin
showDialog(title, cancelOnTouchOutside = true)
```

понятнее, чем

```kotlin
showDialog(title, true)
``` 

Особенно полезными именованные аргументы становятся, когда функция принимает несколько аргументов
одного типа, порядок которых важно не перепутать:

```kotlin
buttonFrameLayout.updateMargins(
    top = topMargin,
    end = endMargin,
    start = startMargin,
    bottom = bottomMargin
)

val zeroDataCell = ZeroDataCell(
    iconResId = R.drawable.ic_zero_data_search,
    titleResId = R.string.doctors_search_idle_state
)

val colorConfig = TextColorConfig(
    normalColor = getColorInt(R.color.text_normal),
    selectedColor = getColorInt(R.color.text_selected),
    disabledColor = getColorInt(R.color.text_disabled)
)
```

Однако в некоторых случаях использование именованных аргументов не оправданно – например, когда
порядок аргументов не играет роли в вычислении результата функции:

```kotlin
// What is the purpose of the named arguments usage in this call? Bad!

val minNumber = min(a = firstNumber, b = secondNumber)
```

```kotlin
// Don't write what you don't need. Good.

val minNumber = min(firstNumber, secondNumber)
```

Во всех остальных случаях именованные аргументы можно использовать свободно:

```kotlin
getInfoUseCase.buildSingle(
    scheduleId = scheduleId, 
    patientTypeId = patientTypeId, 
    appointmentType = appointmentType,
    appointmentDateTime = appointmentDateTime 
)

private var formatter = DateTimeFormatter(
    locale = Locale.getDefault(),
    patterns = EnumMap<DateTimePattern, DateFormat>(DateTimePattern::class.java)
)

private fun initDelegates() {
    delegatesManager 
        .addDelegate(
            PlainTextCaptionWithBodyDelegate(
                onCellClicked = null,
                useCompactVerticalPadding = false
            )
        )
        .addDelegate(
            ZeroDataCellDelegate(
                fillParent = true,
                onButtonClickListener = onZeroDataRetryClick
            )
        )
        .addDelegate(
            MapPreviewDelegate(
                savedState = savedState,
                onMapClicked = onMapPreviewClick,
                onBuildRouteClicked = onBuildRouteClick
            )
        )
}
```

### Функциональные типы

Объявления функциональных типов следуют правилам форматирования, принятым для
[сигнатур функций](#Сигнатура-функции). Примеры:

```kotlin
private val onTemplateChecked: (templateId: Int) -> Unit

var onCategoryChecked: ((categoryId: Int, isChecked: Boolean) -> Unit)? = null

private val onRepeatAppointmentButtonClick: (
    doctorId: Long,
    doctorSpecialities: List<String>
) -> Unit

var onPublicationClick: ((
    bookmarkCell: BookmarkCell,
    publicationCell: BookmarkPublicationCell
) -> Unit)? = null
```

### Тело функции

Как правило, тело функции начинается со следующей строки после её объявления, однако при объемной
сигнатуре допустимо пропускать первую строку для зрительного отделения тела и упрощения
его восприятия:

```kotlin
private fun buildShortcut(
    shortcutId: String,
    navigationTabId: Int,
    destinationIds: List<Int>,
    inAuthorizedGraph: Boolean,
    resetTabToTheRoot: Boolean,
    @StringRes labelResId: Int,
    @DrawableRes iconResId: Int
): ShortcutInfo {

    val intent = Intent(Intent.ACTION_MAIN).apply {
        setClass(context, MainActivity::class.java)
        putExtra(NAVIGATION_TAB_ID, navigationTabId)
        putExtra(IN_AUTHORIZED_GRAPH, inAuthorizedGraph)
        putExtra(RESET_TAB_TO_THE_ROOT, resetTabToTheRoot)
        putExtra(DESTINATION_IDS, destinationIds.toIntArray())
    }
    
    return ShortcutInfo
        .Builder(context, shortcutId)
        .setIcon(Icon.createWithResource(context, iconResId))
        .setShortLabel(context.getString(labelResId))
        .setLongLabel(context.getString(labelResId))
        .setIntent(intent)
        .build()
    }
```

Приветствуется разделение тела функции на логические блоки с помощью пустых строк, а также
комментирование отдельных её участков.

```kotlin
private fun navigateToLoginScreen() {
    val controller = navController ?: return
    val currentDestination = controller.currentDestination ?: return
    
    // Abort navigation if we are already at Login destination.
    if (currentDestination.id == R.id.loginFragment) return

    // Notify User about the forced logout.
    context?.longToast(R.string.login_need_auth_again, 0.1f)

    // Perform logout navigation.
    controller.navigate(R.id.action_authorized_to_login)
}
```

### Пояснительные переменные в функциях

Использование пояснительных переменных с содержательными именами сильно способствуют удобочитаемости функции.

```kotlin
//  Not quite good, large nesting, many indentations.

 override fun markPushAsRead(pushId: String) {
     if (pushId.isBlank()) return

     compositeDisposable.add(
         repository
             .setPushReaded(
                 pushId,
                 SimpleDateFormat(
                     UtcZonedTimeUtils.UTC_DATE_FORMAT,
                     Locale.getDefault()
                 ).format(TrueTimeManager.safeNow())
             )
             .compose(RxUtils.applyIoSchedulersToCompletable())
             .subscribe({
             }, Timber.tag(TAG)::e)
     )
 }
```

```kotlin
// Better.

override fun markPushAsRead(pushId: String) {
    if (pushId.isBlank()) return
   
    val dateFormat = SimpleDateFormat(UtcZonedTimeUtils.UTC_DATE_FORMAT, Locale.getDefault())
    val currentDate = TrueTimeManager.safeNow()
    val formattedCurrentDate = dateFormat.format(currentDate)

    val disposable = repository
        .setPushReaded(pushId, formattedCurrentDate)
        .compose(RxUtils.applyIoSchedulersToCompletable())
        .doOnError(Timber.tag(TAG)::e)
        .onErrorComplete()
        .subscribe()
    
    compositeDisposable.add(disposable)
}
```

### Размер функции

Общие правило – лучше много маленьких функций, чем мало больших.

Считается, что тело оптимально написанной функции не должно быть длиннее **25-30 строк** (без
учёта пустых строк и комментариев). Если тело функции приближается или выходит за этот порог,
вероятно, следует рассмотреть возможность её разбиения на несколько под-функций.

Исключением могут быть функции, содержащие блок **`when`** с длинным списком ветвей, но только
при условии, что этот блок необходим, и функция не может быть реализована по-другому.

Другой важный критерий декомпозиции – атомарность функции. Каждая функция должна выполнять
**только одно логическое действие**, для которого она и была определена. Выход за рамки
одного логического действия означает, что необходимо определить ещё одну функцию.

### Функции-выражения

Функция может быть преобразована в выражение, если она целиком помещается в одну строку.

Примеры:

```kotlin
fun countNonEmptyItems() = items.count { it.isNotEmpty }

fun buildDefaultSelection() = ItemSelection(emptyList())

fun formatPageNumberTitle(page: Int): String = "$pageNumberString: $page" 
```

Если в сигнатуре или теле функции появляется хотя бы один перенос, то функция должна быть
преобразована обратно к блочному виду.

Пример **неправильно** отоформатированной функции:

```kotlin
// Bad.

override fun createDatePickerDialog(
    current: Long,
    minDate: Long,
    maxDate: Long
) = DatePickerDialogFragment.create(this, current, minDate, maxDate)
```
```kotlin
// Ok.

override fun createDatePickerDialog(
    current: Long,
    minDate: Long,
    maxDate: Long
): DatePickerDialogFragment {
    return DatePickerDialogFragment.create(
        activity = this, 
        endDate = maxDate,
        startDate = minDate, 
        selectedDate = current 
    )
}
```

Ещё **анти**-пример:

```kotlin
// Bad.

private fun buildLocalizedTitle() = localizator.localize(
    locale = locale,
    mapStr = dbEntity.titleText,
    fallbackLocale = fallbackLocale
)
```
```kotlin
// Ok.

private fun buildLocalizedTitle(): String {
    return localizator.localize(
        locale = locale,
        mapStr = dbEntity.titleText,
        fallbackLocale = fallbackLocale
    )
}
```

>**Примечание**: исключением из данного правила может являться выражение `= Unit`, используемое
вместо [пустого тела функции](#Пустые-блоки).

Следует избегать длинных и сложносоставных функций-выражений, которые легче воспринимаются
в блочном виде:

```kotlin
// A lot of dots and braces, extension and "apply" operator => hard to understand => Bad.

fun Disposable.untilCleared(): Disposable = this.apply { onClearedDisposable.add(this) }
```

```kotlin
// That's better:

fun Disposable.untilCleared(): Disposable {
    return this.apply { 
        onClearedDisposable.add(this) 
    }
}
```
```kotlin

// That's event better!
// Unnecessary "apply" call is eliminated which made this function cleaner and simplier:

fun Disposable.untilCleared(): Disposable {
    onClearedDisposable.add(this)
    return this
}
```

Для функций типа `Unit` предпочтительной является блочная форма:

```kotlin
// Returning Unit makes it hard to perceive function as an expression => Bad.

@CallSuper
open fun onCleared() = onClearedDisposable.disposeSafely()

fun unregisterLifecycleListener() = ProcessLifecycleOwner.get().lifecycle.removeObserver(this)
```

```kotlin
// Much better.
  
@CallSuper
open fun onCleared() {
    onClearedDisposable.disposeSafely()
}

fun unregisterLifecycleListener() {
    ProcessLifecycleOwner
        .get()
        .lifecycle
        .removeObserver(this)
}
```

## Ссылки на функции

Лямбда-выражение можно заменить ссылкой на функцию:

```kotlin
// Lambda expression passed to the "let" function:

buildMessage()
   .takeIfNotEmpty()
    ?.let {
        displayMessage(message)    
    }
```

```kotlin
// Lambda expression is replaced with function reference:

buildMessage()
   .takeIfNotEmpty()
   ?.let(::displayMessage)
```

Примеры:

```kotlin
// Lambdas are inlined in function calls:

private fun observeViewModel() {
    viewModel
        .selectedTestAccountLiveData
        .observe { testAccount ->
            // Handling test account selection.
        }
        
    viewModel
        .viewStateLiveData
        .observe { loginState ->
            // Handling login state.
        }
        
    viewModel
        .storageInitState
        .observe { storageInitState ->
            // Handling storage init state.
        }
}
```

```kotlin
// Lambdas are replaced with functions references.

private fun observeViewModel() {
    viewModel
        .selectedTestAccountLiveData
        .observe(::handleTestAccountSelection)

    viewModel
        .viewStateLiveData
        .observe(::handleViewState)

    viewModel
        .storageInitState
        .observe(::handleStorageInitState)
}

private fun handleTestAccountSelection(testAccount: TestAccountModel) {
    // Handling test account selection.
}

private fun handleViewState(loginState: LoginViewState) {
    // Handling login state.
}
private fun handleStorageInitState(storageInitState: StorageInitializationViewState) {
    // Handling storage init state.
}

```

Ссылки на функции помогают декомпозировать цепочки вызовов на отдельные операции:

```kotlin
private fun login() {
    loginUseCase
        .buildSingle(phone, password)
        .observeOn(schedulers.ui())
        .subscribeOn(schedulers.io())
        .doOnSubscribe {
            displayProgress()
        }
        .subscribe(
            ::handleLoginResult,
            ::handleLoginError
        )
        .untilCleared()
}

private fun buildDocuments(documentsData: DocumentsData): List<Document> {
    documentsData
        .items
        .asSequence()
        .filter(::filterValidDocuments)
        .map(::mapToDocuments)
        .toList()
}
```

И делают код лаконичнее:

```kotlin
override fun refreshUserAuth(): Single<UserAuthModel> {
    return userAuthStorage
        .getSavedAuth()
        .map { savedAuth ->
            RefreshAuthRequestBody(
                savedAuth.accessToken,
                savedAuth.refreshToken
            )
        }
        .flatMap(apiService::refreshAuth)
        .map(refreshAuthResponseMapper::map)
        .doOnSuccess(::updateUserAuth)
}
```

Ссылки так же работают для функций с двумя и большим числом аргументов, важен только порядок
их объявления:

```kotlin
class AppointmentsListAdapter(
    onZeroDataButtonClicked: () -> Unit,
    onNextPageButtonClick: (currentPage: Int, nextPage: Int) -> Unit,
    onAppointmentAtPositionClick: (position: Int, name: String) -> Unit

) : BaseCellAdapter(AppointmentsListDiffCallback()) {
    
    // Class body.
}

val listAdapter = AppointmentsListAdapter(
    onNextPageButtonClick = ::showNextPage,
    onZeroDataButtonClick = viewModel::reload,
    onAppointmentAtPositionClick = ::showAppointment
)

fun showNextPage(currentPageNumber: Int, nextPageNumber: Int) {
    // Implementation.
}

fun showAppointment(appointmentPosition: Int, appointmentName: String) {
    // Implementation.
}
```

### Ссылки на свойства

Вместо обращения к свойству принимаемого аргумента в лямбда-выражении можно использовать ссылку
на него:

```kotlin
// Referencing properties via keyword "it": 

class Person(
    val age: Int,
    val name: String,
    val isPresent: Boolean
)

fun printNames(people: List<Person>) {
    people
        .filter { it.isPresent }
        .sortedBy { it.age }
        .map { it.name }
        .onEach { name ->
            printPersonName(name)
        }
}
```

```kotlin
// Using property references:

fun printNames(people: List<Person>) {
    people
        .filter(Person::isPresent)
        .sortedBy(Person::age)
        .map(Person::name)
        .onEach(::printPersonName)
}
```

## Цепочки вызовов

Вызов функции на вызове другой функции, обращение к свойству другого свойства и прочие
цепочки вызовов могут быть отформатированы как в виде однострочных выражений, так и в виде
столбцов:

```kotlin
// Singleline chains.

val minLength = viewModel.ehrFormat.minLength

val capitalizedName = name.toLowerCase().capitalize()

val message = result.errorMessage?.toString().orEmpty()
```

```kotlin
// Multiline chains.

viewModel
    .viewState
    .refreshLiveData
    .observe(::handleRefreshState)
    
val firstAvailableDayOfTheWeek = weekModel
    .days
    .indexOfFirst(DayData::isAvailable)
    ?.dayModel
    ?: -1
```

Сложные цепочки следует форматировать в виде столбцов, при этом операторы вызова (**`.`**,
**`?.`**, **`!!.`**) должны образовывать одну вертикальную линию. Такой способ облегчает
зрительное разделение вызовов, особенно если цепочка содержит функции высшего порядка:

```kotlin
// Good formatting.

Single
    .fromCallable { 
        encodePinCodeUseCase.run(pinCode) 
    }
    .flatMapCompletable { encodedPinCode ->
        savePinCodeUseCase.buildCompletable(encodedPinCode)
    }
    .subscribeOn(schedulers.io())
    .subscribe(
        ::handlePinCodeChangeResult,
        Timber::e
    )
    .untilCleared()
```

```kotlin
// What a mess! Bad formatting!

Single.fromCallable { 
    encodePinCodeUseCase.run(pinCode) 
}.flatMapCompletable { encodedPinCode ->
    savePinCodeUseCase.buildCompletable(encodedPinCode)
}.subscribeOn(schedulers.io()).subscribe(
    ::handlePinCodeChangeResult,
    Timber::e
).untilCleared()
```

В столбец рекомендуется выравнивать цепочки **длиннее двух-трёх вызовов**, однако
окончательное решение по форматированию должно приниматься автором кода исходя из:

* его собственной оценки читаемости выражения
* сложившейся в проекте практики: если подобная цепочка уже где-то встречается, нужно
  отформатировать их одинаково.

Примеры правильного *горизонтального* форматирования:
```kotlin
val code = mssage.split(WHITESPACE).find { word ->
    word.isDigitsOnly() && word.length == EXTRACTABLE_CODE_LENGTH
}

mapData.userLocation?.let { userLocation ->
    mapView.showUserLocationMarker(userLocation.lat, userLocation.lng)
}

val newExamsCount = sections.find { it.sectionType == EXAMINATIONS }?.count ?: 0

val doctor = doctorName.takeIfNotEmpty()?.let(::DoctorModel)
```

Примеры правильного *вертикального* форматирования:

```kotlin 
val doctorAvailableTimes = responseBody
    .doctor
    ?.availableTimes
    ?.mapNotNull(::buildAvailableDoctorTime)
    .orEmpty()

private fun observeApiEndpoints() {
    Observable
        .combineLatest(
            apiEndpointsInteractor.observeCurrentEndpoint(),
            apiEndpointsInteractor.observeAllEndpoints(),
            BiFunction(::findSelectedApiEndpoint)
        )
        .observeOn(schedulers.ui())
        .subscribeOn(schedulers.io())
        .subscribe(endpointsViewState::update) { error ->
            Timber.e(error)
            endpointsViewState.set(emptyList())
        }
        .untilCleared()
}

savedState
    ?.getParcelable<CameraState>(STATE_CAMERA_STATE)
    ?.takeIfNotNull()
    ?.let { state ->
        lastCameraState = state as CameraState
    }
```

Пример **неудачного** форматирования:

```kotlin
// Bad.

fun getArticles(params: FeedParams): Observable<MutableList<Item>> {
    return api.getFeed(
        FeedApi.ARTICLES, params.categoryId,
        FeedApi.CHUNK_SIZE, params.offset, FeedApi.CURRENT_API_VERSION
        ).map { it.unwrap() }
        .map { itemsBuilder.build(it) }
        .subscribeOn(Schedulers.io())
        .observeOn(AndroidSchedulers.mainThread())
    }
```

```kotlin
// Much better.

fun getArticles(params: FeedParams): Observable<MutableList<Item>> {
    return api
        .getFeed(
            path = FeedApi.ARTICLES,
            id = params.categoryId,
            from = FeedApi.CHUNK_SIZE, 
            to = params.offset, 
            apiVersion = FeedApi.CURRENT_API_VERSION
        )
        .map(FeedItem::unwrap)
        .map(itemsBuilder::build)
        .subscribeOn(Schedulers.io())
        .observeOn(AndroidSchedulers.mainThread())
    }
```

По возможности следует выносить весь код из сложных цепочек в отдельные методы, чтобы сами цепочки 
были компактными и легко читаемыми:

```kotlin
// Not very good.

override fun getNotificationById(notificationId: String): Single<Optional<AtiNotification>> {
    return notificationsService
        .getNotificationById(notificationId)
        .compose(networkErrorHandler.handleErrorSingle())
        .map { responseDto ->
            val notification = notificationNetworkMapper.mapToDomainModel(responseDto)
            Optional.of(notification)
        }
        .onErrorResumeNext { error ->
            if (error is NotFoundException) {
                Single.just(Optional.EMPTY)
            } else {
                Single.error(error)
            }
        }
}
```

```kotlin
// Better.

override fun getNotificationById(notificationId: String): Single<Optional<AtiNotification>> {
    return notificationsService
        .getNotificationById(notificationId)
        .compose(networkErrorHandler.handleErrorSingle())
        .map(::toOptional)
        .onErrorResumeNext(::resumeOnError)
}

 private fun toOptional(responseDto: AtiNotificationNetworkDto): Optional<AtiNotification> {
     val notification = notificationNetworkMapper.mapToDomainModel(responseDto)
     return Optional.of(notification)
 }
    
 private fun resumeOnError(error: Throwable): Single<Optional<AtiNotification>> {
     return if (error is NotFoundException) {
         Single.just(Optional.EMPTY)
     } else {
         Single.error(error)
     }
 }
```


## Переопределение `set` и `get`

Переопределённый **`get`**'ер неизменяемого свойства рекомендуется располагать на отдельной
строке:

```kotlin
private val hasCameraPermission: Boolean
    get() = requireContext().hasPermission(Manifest.permission.CAMERA)
    
override val objectId: Long
    get() = analysisArgs.analysisId
    
override val isCanceledOnBackPress: Boolean
    get() = dialogArgs.isCanceledOnBackPress
    
val formattedAppointmentDate: String
    get() = dateTimeFormatter.formatDateTime(appointmentModel.date)
```

Двухстрочное написание предпочтительнее, чем однострочное:

```kotlin
val IntArray?.defaultIfNull: IntArray get() = this ?: intArrayOf()  // Not so nice.

val <T> List<T>?.defaultIfNull: List<T> get() = this ?: emptyList()  // Not so nice.

override val listViewModel: SortablePagedEhrListViewModel get() = viewModel  // Not so nice.

val hasLocationPermissions: Boolean get() = locationPermissions.all(::hasPermission) // Not so nice.
```

В примерах выше каждый **`get`**'ер записан в виде функции-выражения. Следуя
[правилам форматирования](#Функции-выражения) таких функций, **`get`**'ер должен быть записан
в блочном виде, если его тело состоит больше чем из одной строки:

```kotlin
val isInputValid: Boolean
    get() {
        return passwordFormat.isValid(oldPasswordInputState.value) && 
                passwordFormat.isValid(newPasswordInputState.value)
    }
    
protected val nestedFragmentManager: FragmentManager?
    get() {
        return childFragmentManager
            .findFragmentById(nestedNavControllerFragmentId)
            ?.childFragmentManager
    }
        
override val arePlayServicesAvailable: Boolean
    get() {
        val result = GoogleApiAvailability.getInstance().isGooglePlayServicesAvailable(context)
        return result == ConnectionResult.SUCCESS
    }
```

Примеры **неправильно** отформатированых **`get`**'еров:

```kotlin
// Wrong.
val attemptsLeftText get() = resourcesManager.getPlural(
    quantity = attemptsLeft,
    displayedQuantity = attemptsLeft,
    pluralsResId = R.plurals.pin_code_attempts_left
)
    
// Wrong.
val isInputValid: Boolean
    get() = passwordFormat.isValid(oldPasswordInputState.value) &&
            passwordFormat.isValid(newPasswordInputState.value)
```

К **`get`** и **`set`** применяются общие [правила форматирования функций](#Форматирование-функций).

Примеры переопределения **`set`**'ера:

```kotlin
var titleText: CharSequence = EMPTY_STRING
    set(value) {
        field = value
        titleView.text = value
    }
    
var selectedPublicationIndex: Int = 0
    set(value) {
        field = value
        if (ignoreChangePublicationCount.not()) {
            publicationsPagerView.currentItem = value
        }
    }
    
var flagColor: String = FLAG_COLOR_UNSPECIFIED
    set(value) {
        if (value.isBlank()) {
            return
        }
       
        val color = try {
            Color.parseColor(value)
        } catch (exc: Exception) {
            Timber.e { "Failed to parse flag color from value \"$value\"\n$exc" }
            null
        }
       
        if (color != null) {
            field = value
            with(flagView) {
                imageTintMode = PorterDuff.Mode.SRC_IN
                drawable.setTint(color)
            }
        }
    }
```

## Аннотации

### Аннотации типов

Аннотации типов всегда располагаются на отдельной строке, предваряющей заголовок типа. Если тип
имеет несколько аннотаций, каждая из них располагается на отдельной строке.

```kotlin
@Module
class SearchHistoryModule {
    // Module implementaiont.
}

@SearchHistoryScope
@Subcomponent(modules = [SearchHistoryModule::class])
interface SearchHistoryComponent { 
    // Component declarations.
}

@AppScope
@Component(
    modules = [
        AppModule::class,
        DataModule::class,
        SearchHistoryModule::class,
        AndroidSupportInjectionModule::class
    ]
)
interface AppComponent : AndroidInjector<ScandinaviaApp> {
    // Component declarations.
}
```

### Аннотации функций

Применяются те же правила, что и для [аннотаций типов](#Аннотации-типов).

```kotlin
@Provides
@LoginScope
fun provideLoginViewModel(
    fragment: LoginFragment,
    loginUsecase: Provider<LoginUserUsecase>
): LoginViewModel {
    return fragment.createViewModel {
        LoginViewModel(loginUsecase.get())
    }
}
```

### Аннотации свойств

В отличие от аннотаций классов и функций, аннотации свойств могут располагаться на той же строке,
что и свойство, если их количество и общая длина не затрудняют восприятие.

```kotlin
// LoginFragment.kt

@Inject lateinit var viewModel: LoginViewModel
@Inject lateinit var navigationHistoryTracker: NavigationHistoryTracker
```

Аннотации аргументов с параметрами следует располагать на отдельной строке, а сами аргументы 
отделять пустой строкой:

```kotlin
class ConfirmAppointmentRequestBody(

    @SerializedName("smsCode")
    val smsCode: Int?,

    @SerializedName("recordId")
    val recordId: Long?,

    @SerializedName("fullName")
    val userFullName: String?,

    @SerializedName("phone")
    val userPhoneNumber: String?,

    @SerializedName("comment")
    val userCommentary: String?

)
```

```kotlin
@GET("/medical-test/")
fun searchForMedicalTests(
    @Query("ehrId") 
    ehrId: Long,
    
    @Query("page") 
    pageNumber: Int,
    
    @Query("search") 
    searchText: String,
    
    @Query("limit") 
    pageSize: Int = PAGE_SIZE
): Single<Response<AnalyzesListResponseBody>>
```

## Блоки управления

### `if else`

Выражение **`if else`** используется для бинарных условий. Если условий больше двух, используется
выражение **`when`**.

Многострочные условия **нежелательны**. Когда это возможно, следует выносить такие условия в
отдельные функции:

```kotlin
// Bad.

val result = if (arg != REFERENCED_VALUE && 
    isFailureConditionSatisfied(arg).not() && 
    arg in MIN_REFERENCED_VALUE..MAX_REFERENCED_VALUE 
) {
    resultFactory.buildResult(param)
} else {
    resultFactory.buildEmptyResult()
}
```

```kotlin
// Good.

val result = if (isConditionSatisfied(arg)) {
    resultFactory.buildResult(param)
} else {
    resultFactory.buildEmptyResult()
}
 
private fun isConditionSatisfied(arg: Long): Boolean {
    return arg != REFERENCED_VALUE && 
            isFailureConditionSatisfied(arg).not() && 
            arg in MIN_REFERENCED_VALUE..MAX_REFERENCED_VALUE
}
```

Скобки вокруг блоков **`if`** и **`else` не опускаются**:

```kotlin
// Awful! Never omit braces!

numbers.forEach { number ->
    if (number.isOdd())
        oddNumbers.add(number)
    else
        evenNumbers.add(number)
}
```
```kotlin
// The only right way to write this "if else" statement:

numbers.forEach { number ->
    if (number.isOdd()) {
        oddNumbers.add(number)
    } else {
        evenNumbers.add(number)
    }
}
```

Пример выражения **`if else`**, за которым следует оператор elvis **`?:`**:

```kotlin
val result = if (isConditionSatisfied(arg)) {
    resultFactory.buildNullableResult(arg)
} else {
    resultFactory.buildEmptyResult()
} ?: DEFAULT_RESULT
```

Блок **`else`** опускается, когда невыполнение условия не требует обработки, либо
когда последним выражением в блоке **`if`** является **`return`**:

```kotlin
private fun confirmAppointment() {
    if (appointmentData.isValid.not()) {
        return
    }
   
    // Confirming appointment.
}
```

Если выражение **`if else`** является коротким, визуально лёгким и простым для понимания,
допускается его однострочное написание. В общем случае предпочтительным должно оставаться
блочное написание.

```kotlin
// Fine.

if (abort) return

val realValue = if (negative) -1L * value else value

var realCode = if (code != -1) code else DEFAULT_CODE

val clinics = getClinics(
    date = Date(),
    doctorIds = if (doctorId != null) arrayOf(doctorId) else null
)

```

Пример нежелательного однострочного написания:

```kotlin
// Too heavy for oneliner! Bad!

val from = if (collapse) widget?.headerView?.height ?: heightExpanded else heightCollapsed
```

```kotlin
// That's better.

val from = if (collapse) {
    widget?.headerView?.height ?: heightExpanded
} else {
    heightCollapsed
}
```

#### Размер блоков `if` и `else`

Если размер функции [не должен превышать 30 строк](#Размер-функции), то блоки **`if`**
и **`else`** должны быть предельно малыми. Если блоки вырастают до 6-10 строк, следует проверить,
можно ли преобразовать выражение в более простое или вынести блоки в отдельные функции.

#### Вложенность блоков `if` и `else`

**В теле блоков `if` и `else` не должно быть вложенных блоков `if`**/**`else` или `when`**.
Такие выражения должны быть вынесены в отдельные функции.

### `when`

Выражение **`when`** используется, когда условий больше двух.

Для бинарных условий всегда используется выражение **`if else`**.

```kotlin
// Bad.
val y = when {
    x >= 0 -> calculateForPositive()
    else -> calculateForNegative()
}

// Bad.
when (checkCondition()) {
    true -> reactForTrue()
    false -> reactForFalse()
}
```

```kotlin
// Good.
val y = if (x >= 0) {
    calculateForPositive()
} else {
    calculateForNegative()
}

// Good.
if (checkCondition()) {
    reactForTrue()
} else {
    reactForFalse()
}
```

Когда это возможно, следует приводить ветви к однострочному виду путём их вынесения
в отдельные функции:

```kotlin
// Not quite good.

val contentData = when (result) {
    is SummaryModel.Success -> {
        val cells = summaryCellsFactory.build(result)
        EhrContentData.Content(cells)
    }
    is SummaryModel.Empty -> EhrContentData.buildEmptyContent()
    is SummaryModel.Error -> EhrContentData.Error
}
```

```kotlin
// Better.

val contentData = when (result) {
    is SummaryModel.Success -> buildSuccessfulContentData(result)
    is SummaryModel.Error -> EhrContentData.Error
    if SummaryModel.Empty -> EhrContentData.buildEmptyContent()
}
```

Перенос после оператора `->` возможен только за открывающей скобочкой блока `{`.

Пример **некорректных** переносов:

```kotlin
// Wrong and terrible wrapping!

when (item) {
    is Item.ARTICLE_ITEM ->
        articleItemsBuilder.buildShareableArticleItemWithPremiumUserContent(item)
        
    is Item.AD_ITEM -> adsDelegate.checkPremiumStatusAndDisplayAd(
       buildAdvertisementItem(item)
    )
    
    is Item.POST_ITEM ->
        // ...
}
```

```kotlin
// Correct wrapping.

when (item) {
    is Item.ARTICLE_ITEM -> {
        articleItemsBuilder.buildShareableArticleItemWithPremiumUserContent(item)    
    }
    is Item.AD_ITEM -> {
        adsDelegate.checkPremiumStatusAndDisplayAd(buildAdvertisementItem(item))
    }
    is Item.POST_ITEM -> {
        // ...
    }
}
```

Если хотя бы одна ветвь блока `when` обрамляется фигурными скобками, все остальные ветви так же должны обрамляться фигурными скобками.
Это создает симметрию и одинаковое выравнивание кода внутри веток, что облегчает чтение и восприятие:

```kotlin
// Wrong.

when (item) {
    is Item.ARTICLE_ITEM -> articleItemsBuilder.buildShareableArticleItemWithPremiumUserContent(item)      
    is Item.AD_ITEM -> {
        adsDelegate.checkPremiumStatusAndDisplayAd(buildAdvertisementItem(item))
    }
    is Item.POST_ITEM -> handlePostItem(item)
}
```
```kotlin
// Correct.

when (item) {
    is Item.ARTICLE_ITEM -> {
        articleItemsBuilder.buildShareableArticleItemWithPremiumUserContent(item)    
    }
    is Item.AD_ITEM -> {
        adsDelegate.checkPremiumStatusAndDisplayAd(buildAdvertisementItem(item))
    }
    is Item.POST_ITEM -> {
        handlePostItem(item)
    }
}
```

Блоки не разделяются пустой строкой.

При проверке принадлежности экземпляра одному из нескольких типов перед каждым типом
ставится ключевое слово **`is`**, независимо от того, является ли тип статическим
(таким как **`object`** либо член типа-перечисления) или динамическим.

```kotlin
when (result) {
    is PossibleResult.Success -> {
        // Branch body.
    }
    is PossibleResult.Error -> {
        // Branch body.
    }
    is SomeEnumType.SOME_ENUM_MEMBER -> {
        // Branch body.
    }
    is SomeObjectType -> {
        // Branch body.
    }
    else -> {
        // Branch body.
    }
}
```

#### Вложенность блоков `when`

**В теле ветвей блока `when` не может быть вложенных блоков `when` или `if`**/**`else`**.
Такие выражения должны быть вынесены в отдельные функции.

### `try catch`

В выражении **`try catch`** не должно быть пустого блока **`catch`**. Как минимум, в нём должен
находиться комментарий, почему данное исключение игнорируется, а сам идентификатор исключения
должен быть назван **`ignored`**:

```kotlin
try {
    performDangerousAction()
} catch (ignored: Exception) {
    // Explanation why handling this exception is unnecessary.
}
```

### `where`

Перечисляемые типы в блоке **`where`** могут либо располагаться на одной строке, либо выравниваться
в столбец – для улучшения читаемости, либо при превышении
[максимальной длины строки](#Ограничение-длины-строки).

Примеры:

```kotlin
// Block "where" is not wrapped.

@Parcelize
class BottomSheetListDialogArguments<T>(
    val title: String,
    val args: List<T>
) : Parcelable where T : BottomSheetCellArgument, T : Parcelable

class ClassWithInheritanceAndBlockWhere<T>(
    val longArgument: Long,
    superClassLong: Long,
    superClassString: String,
    listener: T
    
) : InheritedClass(
    superClassLong,
    superClassString,
    listener
 
) where T: SpecificType, T : AnotherSpecificType, T : Listener {

    // Class body.
}
```

```kotlin
// Block "where" is not wrapped but has wrapped types.
fun <T> createController(
    feedId: Long,
    bookmarkTitle: String,
    listener: T
): EditBookmarkDialogController where T : Controller,
                                      T : BookmarkRenameDialogListener,
                                      T : BookmarkDeleteDialogListener {
    
    // Function body.
}

// Block "where" is wrapped and has wrapped types:
fun <T> createController(listener: T): ProfileEmailChangeDialogController 
    where T : Controller, 
          T : UserNameChangeListener,
          T : UserEmailChangeListener {

    // Function body.
}
```

## Литералы с плавающей запятой

Литералы типа `Float` всегда включают десятичную часть, даже если она равна нулю:

```kotlin
val one: Float = 1.0f
val two: Float = 2.0f
val thirtyFive: Float = 35.0f
```

Данный стиль усиливает визуальное различие между целочисленными литералами и литералами с плавающей
запятой и сохраняет визуальное сходство между числами с нулевой и с не нулевой десятичной частью.

Нулевая целая часть **не опускается**:

```kotlin
val half = .5f  // Bad.
val quarter = .25f  // Bad.
```

## Пустые блоки

Вместо пустой реализации функции можно использовать выражение `= Unit`:

```kotlin 
/*
 * Functions of this interface have default empty implementation,
 * thus they won't be required to be overridden in the inhertinig type.
 */
interface Callback {

    fun onInfoDialogDismiss(requestCode: Int) = Unit

    fun onInfoDialogPositiveButtonClick(requestCode: Int) = Unit

    fun onInfoDialogNegativeButtonClick(requestCode: Int) = Unit

}
```

```kotlin

override fun doSomethingYouNeed(argument: Int) {
    // Non-empty function implementation.
}

override fun dontDoSomethingYouDontNeed() = Unit
```

Выражение `= Unit` допускается переносить:

```kotlin
override fun onBindCell(
    cell: TimeChooseSlotsLoadingCell,
    viewHolder: BaseCellViewHolder
) = Unit
```

В противном случае закрывающая скобка пустого блока размещается на отдельной строке:

```kotlin
override fun wrapBraces() {   // Ok.
}

override fun doNotLeaveBracesOnTheSameLine() {}  // Bad.
```


# Идиоматика языка

## Замена функции свойством `val`

Если функция, возвращающая некое значение, не принимает аргументов и не оказывает побочных
эффектов на объект, на котором она вызывается, то её можно заменить на аналогичное свойство
с переопределённым `get`'ером.

Например, вместо функции

```kotlin
fun Context.getDisplayWidth(): Int = resources.displayMetrics.widthPixels
```

можно определить свойство

```kotlin
val Context.displayWidth: Int
    get() = resources.displayMetrics.widthPixels
```

Аналогично:

```kotlin
val Context.isPortrait: Boolean
    get() = resources.configuration.orientation == Configuration.ORIENTATION_PORTRAIT

val Context.isLandscape: Boolean
    get() = resources.configuration.orientation == Configuration.ORIENTATION_LANDSCAPE

val Context.orientation: Int
    get() = resources.configuration.orientation
    
val View.marginParams: ViewGroup.MarginLayoutParams
    get() = this.layoutParams as ViewGroup.MarginLayoutParams
    
val Fragment.compatActivity: AppCompatActivity
    get() = this.activity as AppCompatActivity
    
val String?.defaultIfNull: String 
    get() = this ?: EMPTY_STRING

val <T> List<T>?.defaultIfNull: List<T> 
    get() = this ?: emptyList()
    
private val isPhoneBlank: Boolean
    get() = phoneInputState.value.isBlank()
    
val CharSequence.trimmedLength: Int
    get() = TextUtils.getTrimmedLength(this)
```

...и так далее.

Важно помнить, что свойство, в отличие от функции, **не характеризует действие**,
поэтому такие функции как `CharSequence?.takeIfEmpty()`, `CharSequence?.takeIfNotNull()` не могут
быть преобразованы в свойства.

## Презумпция нулевой ссылки

Оператор, утверждающий о безопасности вызова (`!!.`), является нежелательным, так как может
быть потенциальным источником `NullPointerException`. Рекомендовано избегать его, насколько это
возможно. Даже если программист считает вероятность возникновения `NullPointerException` в данной
точке выполнения программы минимальной или нулевой, следует учитывать, что данная вероятность может
измениться в будущем при появлении новых условий вызова данного участка кода, а также при переносе
вызова в другую часть программы.

В ситуации, когда после проверки на **`null`** или в блоке **`?.let { }`** происходит ошибка
Smart Cast (не удаётся привести **mutable**-свойство к **Non-Null**-типу), следует выполнять
явное приведение у типу с помощью оператора **`as`**.

Пример:

```kotlin
// ToolbarDelegate.kt

private var toolbar: Toolbar? = null

var onPrepareMenu: ((menu: Menu) -> Unit)? = null
    set(value) {
        field = value
        if (value != null && toolbar != null) {
            /*
             * Compiler error:
             * Smart cast to 'Toolbar' is impossible, because 'toolbar' 
             * is a mutable property that could have been changed by this time.
             */
            value.invoke(toolbar.menu)
        }
    }
```

Т. к. проверка `if (value != null && toolbar != null)` гарантирует, что ссылка `toolbar` не равна
**`null`**, мы можем выполнить её явное приведение к типу `Toolbar`:

```kotlin
if (value != null && toolbar != null) {
    value.invoke((toolbar as Toolbar).menu)
}
```

## Выход из функции с помощью оператора `elvis`

Предположим, для выполнения функции необходимо, чтобы нужное нам свойство не было равно **`null`**.
Первое, что приходит на ум – выполнить обычную проверку:

```kotlin
fun buildRoute(data: LocationData?) {
    if (data?.departmentLocation?.toLatLng() != null) {
        // Function implementation.
    }
}
```

Эта проверка позволяет достичь поставленной цели, однако дальнейшая реализация функции потребует
от нас либо повторять проверку на `null` с помощью оператора `?.`, либо выполнить явное
приведение нужного нам свойства к **`Non-Null`**-типу. Либо и то, и другое.

Конечно, мы можем воспользоваться оператором **`let`**:

```kotlin
fun buildRoute(data: LocationData?) {
    data
        ?.departmentLocation
        ?.toLatLng()
        ?.let { location ->
            // Implementation.
        }
}
```

Однако это приводит к мгновенному росту числа вложенных блоков в теле функции, что усложняет её
чтение. Чтобы сократить код и избавиться от необходимости проверок на **`null`**, можно
использовать следующий способ:

```kotlin
fun buildRoute(data: LocationData?) {
    val location = data?.departmentLocation?.toLatLng() ?: return
    // Function implementation.
}
```

Таким образом мы инструктируем функцию прервать выполнение, если нужное нам свойство рано
**`null`**, и сразу получаем локальный **`Non-Null`**-экземпляр этого свойства.

Этот способ также отлично работает при приведении свойства к типу с помощью оператора **`as?`**.

Примеры:


```kotlin
fun decrypt(toDecrypt: ByteArray, iv: ByteArray): ByteArray? {
    val decryptionKey = getDecryptionKey() ?: return null
    // Function implementation.
}

fun View.adjustHeightToFillParent() {
    val parentViewGroup = parent as? ViewGroup ?: return
    // Function implementation.
}

fun buildDateSpannedString(appointment: AppointmentModel): SpannedString {
    val date = appointment.date ?: return SpannedString(EMPTY_STRING)
    // Function implementation.
}

fun mapToSummary(
    cardsModel: SummaryCardsModel,
    sectionsModel: SummarySectionsModel
): SummaryModel {
    val cards = cardsModel as? SummaryCardsModel.Success ?: throw typeException
    val sections = sectionsModel as? SummarySectionsModel.Success ?: throw typeException
    // Function implementation.
}

fun buildTimeSlotsCell(schedule: Optional<ScheduleModel>): TimeSlotsCell {
    // Here TimeChooseSlotsUnavailableCell is a successor of TimeSlotsCell.
    val scheduleModel = schedule.value ?: return TimeSlotsUnavailableCell
    // Function implementation.
}
``` 

## Аргументы по умолчанию

Не следует использовать аргументы по умолчанию для объединения двух функций в одну,
если такое объединение не может быть обосновано логически, исходя из назначения обех функций.

Ниже – **плохой** пример такого объединения:

```kotlin
/*
 * Has argument Throwable with default value which allows to refer to this 
 * function as "::handleLogoutResult" when no Throwable instance is passed.
 * 
 * Tricky function design – Bad.
 */
private fun handleLogoutResult(error: Throwable? = null) {
    error?.let(Timber::e)
    logoutState.value = LogoutCompleted
}

fun attemptToLogoutUser() {
    logoutUseCase
        .buildCompletable()
        .doOnSubscribe {
            logoutState.value = LogoutStarted
        }
        .subscribeOn(schedulers.io())
        .subscribe(
            ::handleLogoutResult,  // Implicitly using default argument of a function. Unclear!
            ::handleLogoutResult   // Implicitly passing Throwable into function. Awful!
        )
        .untilCleared()
}
```

Здесь должно быть две функции:

```kotlin
// Different function is declared for each of the two actions – Good.

private fun handleLogoutResult() {
    logoutState.value = LogoutCompleted
}

private fun handleLogoutError(error: Throwable) {
    Timber.error(e)
    logoutState.value = LogoutCompleted
}

fun attemptToLogoutUser() {
    logoutUseCase
        .buildCompletable()
        .doOnSubscribe {
            logoutState.value = LogoutStarted
        }
        .subscribeOn(schedulers.io())
        .subscribe(
            ::handleLogoutResult,  // Calling one function in success case – as clear as day!
            ::handleLogoutError    // Calling another function in error case – no ambiguity here!
        }
        .untilCleared()
}
```

## Использование scope функций

TODO: обсудить с командой и дополнить раздел.
https://kotlinlang.org/docs/scope-functions.html#with

# Документирование

## KDoc

Аналогом JavaDoc в языке Kotlin служит KDoc:

```kotlin
/**
 * KDoc комментарий.
 */
```

Документ пишется по-русски, с соблюдением правил орфографии и грамматики языка.

Все комментарии, располагающиеся над свойствами, функциями и типами, форматируются в виде KDoc:

```kotlin
// Bad.

// Публичная функция не должна документироваться с помощью обычного комментария, такого как этот. 
fun getNotifications(request: AtiNotificationsRequest): Single<List<AtiNotification>>
```

```kotlin
// Good.

/**
 * KDoc гораздо полезнее. Он позволяет добавлять ссылки на классы и функции, давать описание 
 * параметрам, свойствам и прочее.
 *
 * @param request объект запроса списка АТИ уведомлений.
 */
fun getNotifications(request: AtiNotificationsRequest): Single<List<AtiNotification>>
```

>**Примечание**: чтобы ссылки на публичные типы отобразились в KDoc, необходимо добавить в файл
директивы **import** с соответствующими типами.

## Комментарии

Так же как и KDoc, обычные комментарии пишутся на русском языке, с соблюдением правил 
орфографии и грамматики.

### Форматирование комментариев

Каждый комментарий начинается с **пробела** и завершается **точкой**.

Для комментариев длиной до 4 строк можно использовать двойной слэш `//`:

```kotlin
// Данный exclude был добавлен, чтобы решить проблему дублирующихся файлов META-INF.
// На работоспособность приложение это повлиять не должно.
// https://stackoverflow.com/questions/44509608/duplicate-files-copied-in-apk-meta-inf-library-release-kotlin-module
```

При желании, для комментариев длиннее 2 строк можно использовать звёздочки `/* */`. В этом
случае первая и последняя строка комментария остаются пустыми:

```kotlin
/**
 * Данный exclude был добавлен, чтобы решить проблему дублирующихся файлов META-INF.
 * На работоспособность приложение это повлиять не должно.
 * https://stackoverflow.com/questions/44509608/duplicate-files-copied-in-apk-meta-inf-library-release-kotlin-module
 */
```

Для однострочных комментариев звёздочки **не используются**:

```kotlin
/* Неправильно оформленный однострочный комментарий. */   // Bad.

/*
 * Неправильно оформленный однострочный комментарий.      // Bad.
 */
```

Комментарии так же подчиняются [лимиту символов в строке](#Ограничение-длины-строки).

#### При написании комментариев помним несколько простых НЕ:

* Комментарии **не** дублируют код.
* Комментарии **не** содержат недостоверных сведений и **не** могут привести к ошибочной
  интерпретации кода.

### Закомментированный код

Нахождение в проекте закомментированных кусков кода не приветствуется, так как для этих целей
служит VCS. Исключением может быть ситуация, когда судьба кода решается в кратчайший промежуток
времени, и до той поры его присутствие в закомментированном виде не вызывает неудобств
у участников проекта. Закомментированные участки обязательно должны сопровождаться инструкциями
`// TODO` с пояснением причины комментирования, условий раскомментирования и
примерных сроков принятия решения. Смотри [правила по оформлению TODO](#Инструкции-TODO).

### Комментарии-разделители

Для удобства чтения и навигации по классу его тело можно разделить на регионы с помощью
специальных комментариев `// region <Region Name>` и `// endregion`. При этом такие комментарии
отделяются от кода пустой строкой изнутри и двумя пустыми строками – снаружи:

```kotlin
private val nonSpecificProperty = 1.0f


// region Specific class region

private val specificProperty = calculateSpecificProperty()

private fun performSpecificAction() {
    // ...
}

// endregion
```

Если за закрывающим комментарием `// endregion` следует открывающий комментарий `// region`, то
между ними также остаётся 2 пустых строки:

```kotlin

// region Lifecycle

override fun onStart() {
    trackScreenStart()
    // ...
}

override fun onEnd() {
    // ...
}

// endregion


// region Analytics

private fun trackScreenStart() {
    // ...
}

private fun trackButtonClick() {
    // ...
}

// endregion

```

### Комментарий TODO

Запланированный технический долг и критические проблемы в коде нужно помечать с помощью комментария TODO.

Комментарий TODO должен иметь следующий формат:
```kotlin
// TODO Автор: {name}, дата: {date}, задача: {task}
//  {text} 
```
Где:
* `{name}` - кто обнаружил проблему;
* `{date}` - дата заведения TODO;
* `{task}` - номер задачи, в рамках которой будет устранена проблема;
* `{text}` - описание TODO.

В многострочных TODO комментариях ко всем строчкам после первой добавляется отступ. 
**Не нужно** добавлять TODO к каждой строке:
```kotlin
// TODO Автор: Суринов, дата: 02.03.2022, задача: ADNR-1000
//  Вынести этот код в общий модуль.
//  Добавить юнит тесты.
```

Два важных условия:

* Инструкции не должны быть очевидными.

* `TODO` не должен находиться в проекте вечно. В идеале такой комментарий должен быть максимально
  краткосрочным. Если `TODO` указывает на запланированный технический долг, требующий согласования
  с менеджером, то по нему должен появиться срок закрытия и задача.

Быстро перемещаться по оставленным `TODO` в Android Studio можно с помощью специального окна,
которое открывается вот так:

**View** -> **Tool Windows** -> **TODO**.

# Ссылки на источники

* [JetBrains Kotlin Coding Conventions](https://kotlinlang.org/docs/reference/coding-conventions.html)
* [Google Kotlin style guide](https://developer.android.com/kotlin/style-guide)
* [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
