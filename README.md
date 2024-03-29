## Проект CustomCollections

Предоставляет словарь для хранения элементов имеющих уникальный составной ключ [Id, Name]. Компоненты ключа могут быть произвольного типа, содержащимися в объектах.

Тип компонентов определяется при объявлении.

Указанный словарь реализован в классе `CompositeKeyDictionary<TId, TName, TValue>`. Здесь, `TId` определяет тип компоненты `Id` составного ключа, `TName` - соответственно тип компоненты `Name`. `TValue` определяет тип элементов словаря. 

**Внимание**: данная реализация словаря **не является потоко-безопасной**. При использовании параллельно из нескольких потоков высока вероятность коллизий.

В классе реализованы методы для получения/удаления всех элементов по Id или Name. Это методы `IReadOnlyCollection<TValue> GetValuesById(TId id)` и `IReadOnlyCollection<TValue> GetValuesByName(TName name)`. Внутреннее устройство словаря позволяет получить доступ к коллекции составных ключей по одной из его компонент за 1 операцию. Далее элементы, соответствующие полученным на предыдущем шаге ключам возвращаются в виде коллекции только-для-чтения. 


---


##Тестовый проект CustomCollections.Tests
В тестовом проекте в классе `CompositeKeyDictionaryTests` собраны тесты основных методов класса `CompositeKeyDictionary<TId, TName, TValue>`.

В каждом тесте используется словарь элементов `User`, в котором компонента ключа `Id` представлена пользовательским типом `UserId`.

В классе `UserId` переопределены методы `GetHashCode` и `Equals` с целью реализовать сравнение экземпляров этого класа по значению.

---