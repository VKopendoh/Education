## Сессия пользователя
1. Регистрация
2. Авторизация
3. Игра
4. Выход

### Решистрация
**Frontend**
- Страница с вводом email, login и passsword

**Backend**
- Сервлет обработки запроса
- Класс AccountService с методом регистрации
- Класс UserProfile с полями: login, email, password
- Карта <login, UserProfile>

### Авторизация
**Frontend**
- Страница с входом: login, password

**Backend**
- Сервлет обработки запроса
- Класс AccountService с методом авторизации
- Поиск UserProfile в карте по login
- Карта <HTTPSession, UserProfile>

### Учетная запись 
**Frontend**
- Страница после логина

**Backend**
- Сервлет обработки запроса страницы
- Получение HttpSession из request-a
- Поиск UserProfile в карте по HttpSession

### Выход
**Frontend**
- Кнопка выхода

**Backend**
- Сервлет обработки запроса 
- Получение HttpSession из requst-a
- Удаление UserProfile в карте из HttpSession

## Generics
Generic programming - тип переменной как параметр

**Проверка типов во время компиляции**
- вставка разных типов в runtime 
- нет необходимости в использовании ключевого слова cast

**Универсальные алноритмы**
- N алгоритмов, M типов данных = N на M реализаций
- алгоритмы работают с шаблонами => N реализаций

**Упрощение кода**
- меньше кода
- понятнее

### Класс с generic типом
``` java
public class GenericExample<T> {
	private T value;

	public GenericExample(T value) {
		this.value = value;
	}

	public T getT() {
		return value;
	}

	public static void main (String[] args) {
		GenericExample<Integer> intObjec = new GenegicExample<>(1);
		Integer valueInteger = intObject.getT();

		GenericExample<String> stringObject = new GenericExample<>("word");
		String valueString = stringObject.getT();
	}
}

### Метод с generic типом
``` java
public class GenericExample {
	public static <T> T getFirst(List<T> list) {
		list.get(0);
	}

	public static void main (String[] args) {
		List<Integer> listOfInts = new ArrayList<>();
		listOfInts.add(0);
		Integer intValue = getFirst(listOfInts);

		List<String> listOfStrings = new ArrayList<>();
		listOnStrings.add("Java");
		String stringValue = getFirst(listOfStrings);
	}
}

### Типизация generic значений 
``` java
public static Object getFirstValue(List list) {
	return list.get(0);
}

public static String getFirstStringValue(List<String> list) {
	return list.get(0);
}

public static void main (String[] args) {
	List<Intger> listOfNumbers = new ArrayList<>();
	listOfNumbers.add(42);

	String name1 = (String) getFirstValue(listOfNumbers); // Runtime error
	String name2 = getFIrstStringValue(listOfNumbers); // Compile error
}

### Generics. Примеры синтаксиса
- List<String> students = new ArrayList<String>();
- Map<Integer, String> indexToName = new HashMap<Ingeger, String>();
- void printCollection (List<Integer> collection) { ... }
- void orintCollection (List<?> collection) { ... }
- void drawShape (List<Shape> shapes) { ... }
- void drawShape (List<? extends Shape> shapes) { ... }

### Сужение области параметра
``` java
public class GenericExample <T extends Number> {
	private T value;

	public GenericExample (T value) {
		this.value = value;
	}

	public T getT() {
		return value;
	}

	public static void main (String[] srgs) {
		// Integer extends Number -> OK
		GenericExample<Integer> intValue = new GenericExample<>(1);
		Integer value = intValue.getT();

		// String does not extend Number -> ERROR
		GenericExample<String> stringNumber = new GenericExample("word");
		String value = stringValue.getT();
	}
}

### Специфическое использование
- Использование без типизации - deprecated
List
Можно передавать - List<Object>, ArrayList<Integer>, LinkedList<String> ...
- Использование Object в качестве параметра 
List<Object> 
Можно передвать коллекции только от Object
- Произвольный тип в качестве параметра
List<?>
Можно передавать любые коллекции, но вставка не возможна 

### Wildcards
- List<? extends Number> 
Можно передавать List<Integer>, ArrayList<Long>, LinkedList<Number> ...
- List<? super Integer>
Можно передавать List<Integer>, ArrayList<Number>, LinkedList<Object> ... 

### Generics vs inheritance
**Наследование**
Принцип "разновидность чего-то" (is a)

**Шаблон**
Принцип "специализируется на" (of something)

Пример:
class Ветеринар<T extends Животное> extends Человек 
T: слон, собака ... 
В случае Т: Человек, получаем ветеринара по людям - врача

### class LongId<T>
Для того, что бы при написании сервера не запутаться с Id сущностей, для удобства можно использовать generic-class LongId<T>.
``` java
public class LongId<T> {
	private long id;
	
	public LongId(long id) {
		this.id = id;
	}

	public long getLong() {
		return id;
	}
}

public void manyIdsInParams(long userId, long serverId, ....) { ... }

public void manyIdsInParams(LongId<User> userId, LongId<Server> serverId, LongId<Address> addressId, ...) { ... }

## Коллекции и карты
### Iterator и Iterable
Iterator - то, что мы можем получить для любой коллекции.
Что бы коллекция могла вернуть iterator, она должна реализовывать интерфейс Iterable.
**Interface Iterator<T>**
- boolean hasNext();
- T next();
- void remove();

**Interface Iterable<T>**
- iterator<T> iterator();

### Collection
**Методы**
- add(T object);
- addAll(T object);
- clear();
- contains(Object obj);
- remove(Object obj);
- removeAll(Collection<T> colection);
- size();
- isEmpty();

### List, Set, Queue
**List**
- список с очередностью
- LinkedList - быстрое удаление и добавление элементов
- ArrayList - быстрый доступ по индексу

**Set**
- без очередности 
- без индекса
- быстрый поиск элемента 

**Queue**
- FILO

### Map
**Map<key, value>**
- быстрый поиск по ключу 
- объект в качестве value. Например другой контейнер - Map<Integer, List<Integer>> 
[видео про map](https://stepic.org/lesson/%D0%9A%D0%BE%D0%BB%D0%BB%D0%B5%D0%BA%D1%86%D0%B8%D0%B8-%D0%B8-%D0%BA%D0%B0%D1%80%D1%82%D1%8B-12401/step/7?unit=2831)

### Comparable
**Interface Comparable<T>**
Используется для сравнения своих типов данных, например для сортировки коллекций. 
int compareTo(T obj);
Возвращаемое значение можеть быть >, =, < 0

Пример:
``` java
Integer a = 1;
Integer b = 2;

a.compareTo(b) == -1; // true
a.compareTo(a) == 0; // true
b.compareTo(a) == 1; // true

### class Collections
Набор статических методов для работы с контейнерами.

**Основные методы**
- void copy(List dest, List src);
- Object max(Collection collection);
- Object min(Collection collection);
- void reverse(List list);
- void shuffle(List list);
- void sort(List list);
- void swap(List list, int i, int j);

### Classloader
Classloader - часть JVM, которая загружает данные о классах.
Все классы должны быть загружены при старте JVM.

JVM перед тем как начать работать с байткодом необходимо загрузить в память данные о всех классах. Когда мы загружаем в память информацию о классах, мы эту информацию храним в виде неких объектов. 

При старте JVM работают следующие загрузчики, которые работают друг за другом:
- Bootstrap class loader (<JAVA_HOME>/jre/lib)
- Extensions class loader (<JAVA_HOME>/jre/lib/ext)
- System class loader (CLASSPATH)

### java.lang.Class
java.lang.CLass - это класс, объекты которого описывают классы из нашей библиотеки (приложение) и firdparty. 
Class - объект, который представляет в runtime данные о классе объекта. 
Класс — тип
Объект — объект некоторого типа
Но на класс можно смтреть как на объект метакласса  содержащего информацию полях, методах, константах и прочем.

**Основные методы Class**
- static Class<T> forName(String className);
- String getCanonicalName();
- Fields[] getFields(String name);
- Class[] getInterfaces();
- Method[] getMethods();
- Constructor[] getConstructors();

### class Object
class Object - класс от которого унаследованы все остальные классы.
- class MyClass{..} == class MyClass extends Object{...}
- void myFunction(Object varName) - может "обработать" любой объект

**Основные методы класса Object()**
- public Class<?> getClass();
- public String toString();
- public boolen equals(Object obj);
- public int hushCode();
- protected Object clone();

### Примитивные типы
bits | type | type
 8   | byte | boolean
 16  | short| char
 32  | int  | float
 64  | long | double 

### Обертки простых типов
**boolean, byte, short, char, int, float, long, double**
Примитивные типы:
- мало памяти 
- простая структура (ячейка в памяти)
- Stack

**Byte, Boolean, Short, Character, Integer, Float, Long, Double**
Обертки простых типов:
- наследники от Object
- сложные типы
- Heap

### Массивы и Строки
**Массив**
- массив это объект (наследник от Object)
- массив хранит свой размер (new int[10]).lenght;
- переменная может быть размером массива

Для работы с массивами можно использовать класс Arrays

**Строки**
- обертка на д массивом char[]
- char - 16 bit (UTF-16)
- immutable: "abc" + "bcd" - создание новой строки

### Size of Object
Точный размер объекта зависит от:
- версии Java
- издателя (Oracle JDK, open JDK...)
- разрядности OS
- параметров запуска JVM

Размер объекта состоит из:
- object header (8 byte)
- размер примитивных типов
- размер ссылок (32 или 64 bit на ссылку) 
+ гранулярность 8 byte
