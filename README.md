# Правила и рекомендации по комментированию в коде

Всем привет! Сегодня я хочу представить статью о правилах комментирования в коде. Я не хочу сказать, что рекомендации, представленные в данной статье, являются аксиомами. Нет, всегда найдутся две стороны: на одной стороне всегда будут те, кто согласен с представленными рекомендациями, на другой - те, кто не согласен. Разнообразие мнений — это нормально и прекрасно.

![image](https://user-images.githubusercontent.com/43491660/144230501-be39ec12-381e-4e4f-a455-de4955fa674c.png)


Моё мнение, отражённое в данной статье, основывается на книге «Чистый код» Роберта Мартина.

## Неужели хороший код не нуждается в комментариях?

Какой код можно назвать хорошим? Все мы стремимся писать хороший код, но не всегда можем объяснить, что это такое. Обычно хорошим называют самодокументированный, самопоясняющиий код, то есть в нём должно быть понятно, что и как происходит. Ведь ничто не может пояснить код, лучше самого кода. Но бывают ситуации, когда без комментирования не обойтись. Я приведу несколько примеров хороших и плохих комментариев.

### Хорошие комментарии

Если эти комментарии присутствуют в вашем коде — это хорошо.

#### Юридические комментарии
Корпоративные стандарты написания кода могут требовать оставлять комментарии по юридическим соображениям. Например, заявление о юридических правах. Эта информация обязательно размещается в комментарии в начале каждого файла с исходным кодом. Такие комментарии не должны иметь вид трактата, достаточно указать суть, сослаться на лицензию или другой внешний документ. 

Например:

```
animate.css - https://daneden.github.io/animate.css/
Version - 3.7.2 
Licensed under the MIT license - http://opensource.org/licenses/MIT

Copyright (c) 2019 Daniel Eden

```
Большинство IDE позволяют автоматически сворачивать подобные блоки комментариев, чтобы они не загромождали остальной код. 

#### Информативные комментарии
Содержат пояснения к сложной для восприятия части кода. Наиболее полезны информативные комментарии с регулярными выражениями, потому что разработчику очень сложно сходу понять, какой шаблон зашифрован в регулярном выражении. Эти комментарии сэкономят время разработчиков, которые захотят понять, что делает этот код. Не дай другому программисту надолго зависнуть над этим участком кода!
Например:
```
// Поиск по формату: kk:mm:ss EEE. MMM dd. yyyy
сonst timeMatcher = new RegExp('\\d*:\\d*:\\d* \\w*. \\w* \\d*. \\d*');

```


Ещё такой комментарий можно использовать, когда вы наткнулись на запутанную часть кода. Если фрагмент кода достаточно сложный, а времени на рефакторинг в данный момент нет, лучше оставить подобный комментарий. Тогда в следующий раз вы или другой разработчик потратите меньше времени, чтобы разобраться в этом коде. 
Если вы уже потратили время на то, чтобы разобраться в сложном коде, имеет смысл оставить комментарий с пояснениями для коллег.

![6d593bd0f807039be85e54b5fbc5fdbf](https://user-images.githubusercontent.com/43491660/144230909-ff1dca9a-dc4c-4077-9e3c-8672eca8d446.jpg)


#### Прояснение, представление намерений, пояснения к поведению

Иногда бизнес-требования ставят перед программистами задачи, решение которых трудно сделать интуитивно понятным для других разработчиков, если они не читали требования к задаче. Такие комментарии добавляют контекст к не интуитивному решению, помогают разобраться с деталями кода, описывают намерения, заложенные в решении. Например, когда проводится работа с библиотекой, неочевидна бизнес-логика или описываются особенности в браузере IE.

Как бы разработчик не старался, такой код не сможет ответить на вопрос "почему здесь сделано именно так". Такие комментарии позволят облегчить работу тех, кто будет заниматься поддержкой, рефакторингом или расширением кода в дальнейшем. Разработчики обязательно скажут вам спасибо!

Такие комментарии часто помогают объяснить магические числа в коде.
Например:

```
// Для дополнительных задач требуется добавлять префикс перед идентификатором, чтобы он не совпадал с каким-либо из id выездов
orderStateDTO.setOrderId("f_" + additionalTask.getId());

```

#### Комментарии **TODO** 

Содержат пометки на будущее, информацию о том, что важно сделать, но не сейчас. Например, когда в будущем нужно сделать какой-то рефакторинг или сделать что-то, когда будет реализована зависимая часть кода. Большинство IDE, позволяют вывести эти комментарии TODO в отдельное окно, что очень удобно.

После реализации основной логики какой-то задачи, можно вернуться к таким комментариям и реализовать то, что ещё не было сделано, но необходимо. То есть получаем чек-лист на будущую работу, чтобы не искать потом по всему коду то, что вы забыли дописать. Это классический вариант технического долга. Можно больше не записывать себе задачки на листочке, а писать их прямо в коде!

Например:

```
// TODO: Удалить после удаления класса GroupTaskPanel
// TODO: Проверить логику с приходящим значением null
```

Проблема таких комментариев в том, что они редко просматриваются и не актуализируются. Поэтому, если вы используете такие комментарии, просматривайте их периодически и удаляйте ненужные. 

#### Комментарии Jsdoc в общедоступных API (Это актуально также для аналогичных инструментов документирования в других языках)
Если код хорошо документирован в общедоступном API с ним приятно и легко работать. В таком случае рекомендуется писать комментарии, которые будут упрощать формирование документации. Это документация метода или класса, которая показывается, когда вы генерируете документацию из вашего кода или когда вы наводите мышкой на название метода и там показывается его Jsdoc (необходимые параметры, их типы, возвращаемое значение).

Jsdoc стоит использовать только с public методами и никогда с private методами. Private методы могут меняться без предупреждения и в общедоступной документации они не описываются.

Например:

```
/**
 * Складываем числа
 * 
 * @param {number} first - первое число
 * @param {number} second - второе число
 * @returns {number}
 *
 */  
function add(first, second) {
        return first + second;
}

```

#### Усиление

Комментарий такого рода подчёркивает важность обстоятельств, которые неочевидны с первого взгляда. Комментарий обращает внимание на то, что делает код, и на то, что его нельзя удалять. Свидетельствует о том, что код играет важную роль. Ведь всегда найдётся инициативный джун, рвущийся зарефакторить код и удалить пару лишних строчек:)

Например:

```

// Вызов trim() важен. Он удаляет начальные пробелы, чтобы строка успешно интерпретировалась как список
let listItemContent = match.group(3).trim();

```

#### Предупреждение о последствиях

Это важные пояснения, которые предупреждают о том, что могут возникнуть проблемы после внесения определённых исправлений. Это как оберег к вашему коду от плохих изменений, чтобы потом не ломать голову, что же сломалось?!

Например:

```
// Don't lower more than 500ms, otherwise there will be animation-problems with the Safari toolbar
setInterval(function() {
	$(window).scrollTop(-1);
	resize();
}, 500);
```



### Плохие комментарии

#### Бормотание или непонятные комментарии, шум

Чаще всего такие комментарии оставляют те, кто не умеет чётко формулировать свои мысли или не понимают, зачем вообще нужны комментарии в коде. Такие комментарии содержат возмущения разработчика или просто его реакцию на какую-то часть, но никак не помогают улучшить код. Некоторые разработчики пытаются разбавить код шуткой, чтобы разрядить обстановку, но этим они только засоряют код и делают его труднее для чтения.
Например:

```

// WTF????? Refactor this!
// Не грусти, я тоже не понимаю, что здесь происходит:(

```

 ![image](https://user-images.githubusercontent.com/43491660/144230826-bb8f3bd2-ac6b-41b3-aec7-a8200959001b.png)

#### Избыточные комментарии

В комментарии не должно быть абсолютно однозначной по коду информации. Лучше не использовать комментарии, которые дублируют функциональность кода и не пытаться добавить ясные лексические конструкции самого кода. 

Такие комментарии обычно дублируют и без того понятные строки кода. Они только отнимают время на то, что можно понять непосредственно из самого кода. Такие пояснения не улучшают код и не делают его удобочитаемым. Если комментарий ничего не проясняет, то он не нужен.

Например:

```

// вспомогательный метод: возвращает деление двух чисел, когда второе не равно 0
function numbersDivision(a,b) {
    // Если знаменатель равен 0, то возвращается null
    if(b==0){
	return null;
    }

    // результат метода
    return a/b;
}

```

#### Журнальные комментарии, ссылки на авторов

Нередко разработчики указывают, в рамках какой задачи были исправлены те или иные строки. На самом деле современные системы Git и IDE позволяют узнать, кем и в рамках какой задачи изменён код. Данные о правках можно найти в системе контроля версий. К тому же зачастую рефакторинг происходит в рамках других задач, и комментарий становится недостоверным. 
Когда разработчик видит такой комментарий к методу, который ему нужно поправить, он начинает сомневаться, нужно ли его править и зачем здесь комментарий, а вдруг здесь что-то не так? Не надо так.

```
// Добавлено Иваном
// Измненено в рамках задачи Task-675
// Поправлено 05.10.2019

```

#### Закомментированный код

Если вы решили закомментировать код вместо того, чтобы от него  избавиться, то лучше не стоит. Закомментированный код накапливается, а коллеги могут не удалять его, думая, что он важен. Не стоит складировать старый код, если можно в любой момент в системе контроле версий посмотреть нужную версию и вернуть необходимый участок кода. Удалять закомментированный код стоит целиком.

Окружение постоянно подвергается рефакторингу, а закомментированный код не меняется и теряет свою актуальность. Когда вы захотите его раскомментировать, он будет абсолютно непонятен из окружающего кода, и даже может не компилироваться, так как вокруг будут уже совсем другие переменные и методы. И тогда мы идём к системе контроля версий, чтобы понять, что и зачем там было. Лучше добавить комментарий в Git, зачем был удалён тот или иной блок кода.

#### Позиционные маркеры

Часто в комментариях разработчики используют слэши, минусы, звёздочки и пр., пытаясь таким образом отделить блоки кода. Если вам захотелось отделить блок кода, значит пора выделить его в отдельный метод.

Например:

```
///////////////////////////////////////////////////////////////////
********************** комментарий **********************************
```

#### Комментарии за закрывающейся фигурной скобкой

Такие комментарии часто используют, когда пишут большие циклы или условия, и довольно сложно отследить, где заканчивается тот или иной блок кода. Комментарии часто пишут после фигурных скобок блоков while, try, if и пр. 
В процессе рефакторинга эти скобки съезжают и обозначают уже конец другого блока, что может запутать разработчика. Любая современная IDE позволяет «схлопнуть» блок кода и увидеть, где его начало и конец. Если строчек действительно много — это хороший знак, что надо вынести часть кода в отдельный метод, чтобы повысить удобочитаемость.

 Например:

```

try{

   while (что-то){

        много строчек

    } // while 

   много строчек

 } // try

```

#### Недостоверные комментарии

Самый распространённый пример недостоверных комментариев - устаревшие комментарии. При рефакторинге кода разработчики забывают обновлять комментарии к нему, чем вводят в заблуждение своих коллег. Такие комментарии пишутся на скорую руку. Например, специалист не до конца разобрался в коде или написал сначала комментарий, потом реализовал функцию, а после решил поменять логику функции, забыв про комментарий. В таком случае комментарий уже недостоверен. 

#### Обязательные комментарии

Некоторые компании заставляют разработчиков писать комментарии, считая, что код будет понятнее. Это неправильно. Это создаёт лишний мусор и не улучшает качество кода. Гораздо более продуктивно заставлять разработчиков правильно называть функции и классы, чем писать комментарии.


## Заключение

Я считаю, что главное — это понимать, что комментарий не улучшит плохой код. Если очень хочется написать над методом то, что он делает, подумайте, может из этого текста комментария сделать название этого метода, сократив и оставив важную часть, тогда этот комментарий и вовсе не понадобится. В большинстве случаев ваши намерения должны быть видны из кода, а не из комментариев.

Есть несколько тезисов из книг, которые, на мой взгляд, лучше всего отображают мнение автора о комментариях:

- Не комментируйте плохой код – перепишите его
  - Код должен говорить сам за себя
- Комментарии не являются «абсолютным добром»
  - Код развивается, а комментарии - нет
- Комментарий – признак неудачи
  - У вас не получилось написать код так, чтобы его можно было понять без комментариев
- Комментарии не компенсируют плохого кода
  - Каким бы хорошим ни был комментарий, он не оправдывает плохой код
- Хороший комментарий – объяснение своих намерений в коде
  - комментарий должен отвечать не на вопрос "что делает код", а на вопрос "зачем"
- По-настоящему хороший комментарий – тот, без которого вам удастся обойтись
  - Лучше делать код понятным сразу, чем пытаться объяснить его с помощью комментариев


