# Компоненты
Компонент - объединение набора типов, по некоторым характеристикам.

К примеру:
Можно создать компонент регистрации, в который входят такие типы, как класс для показа окна регистрации, класс для работы с сервером регистрации, вспомогательные классы.

Компоненты могут быть выкинуты из библиотеки, и служат лишь для упрощения работы с большими приложениями.

## Объявление
прежде чем использовать компонент, его нужно объявить. Так как компонент является следующей ступенью над типом, а тип в библиотеке представляется в виде набора функций, логично представить компонент в виде функции. Но функция не может быть легко использована само по себе, поэтому создается класс с единственной функцией. Чтобы объявить компонент нужно:
* Создать свой класс
* Объявить, что класс реализует протокол `DIComponent`
* Реализовать метод `load(builder: DIContainerBuilder)`

```Swift
class RegistrationComponent: DIComponent {
  func load(builder: DIContainerBuilder) {
    builder.register...
  }
}
```
Слово builder вам уже знакомо из прошлых глав.

## Регистрация
После того как мы объявили компонент, его нужно зарегистрировать для дальнейшего использования:
```Swift
builder.register(component: RegistrationComponent())
```
Регистрация компоненты, не сильно отличается от регистрации типа, но в функцию регистрации добавляется ключевое слово `component`. Помимо этого стоит обратить внимание на то, что регистрирует не класс, а экземпляр класса. На самом деле сколько бы раз не был бы создан экземпляр компонента, при регистрации он будет учитываться только один раз.

## Область видимости
Использование компонент предполагает и использование модулей, о которых написано в следующей главе, хотя и не обязывает. По этой причине у компоненты можно объявить область видимости, в которой данный компонент будет виден: `internal` или `public`. 
В случае с `internal` это будет означать, что компонент виден только внутри текущего модуля. `public` же означает, что компонент виден и за пределами модуля.
Чтобы изменить область видимости, которая по умолчанию является `internal` надо определить свойства `scope` у компоненты:
```Swift
class RegistrationComponent: DIComponent {
  var scope: DIComponentScope { return .public }
  ...
}
```

#### [Главная](main.md)
#### [Предыдущая глава "Время жизни"](lifetime.md#Время-жизни)
#### [Следующая глава "Модули"](module.md#Модули)