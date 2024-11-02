# Задача "Понимание JVM"

## Описание
Просмотрите код ниже и опишите (текстово или с картинками) каждую строку с точки зрения происходящего в JVM  

Не забудьте упомянуть про: 
- ClassLoader'ы, 
- области памяти (стэк (и его фреймы), хип, метаспейс)  
- сборщик мусора

## Код для исследования
```java

    public class JvmComprehension { 
    // Class Loaders загружают класс JvmComprehension и все системные классы в область Metaspace

        public static void main(String[] args) { 
        // Создание нового фрейма в области Stack Memory
            int i = 1;                      
            // 1 Инициализируется примитивная переменная i, присваивается 1, она добавляется в Stack Memory
            
            Object o = new Object();        
            // 2 Создаётся объект класса Object в куче (Heap), в Stack заводим ссылку o, связываем её с объектом
            
            Integer ii = 2;                 
            // 3 Создаётся объект класса Integer в куче, у объекта значение 2, ссылка на него записывается в ii
            
            printAll(o, i, ii);             
            // 4 Создание нового фрейма в области Stack для данного метода
            
            // Когда выполнение метода закончится, стек автоматически удаляет фрейм для данного метода
            System.out.println("finished"); 
            // 7 В куче создаётся объект класса String со значением "finished", и ссылка на него передастся в метод println(), для которого создастся новый фрейм
            
        }

        private static void printAll(Object o, int i, Integer ii) {
            Integer uselessVar = 700;                   
            // 5 Создаётся объект класса Integer в куче, у объекта значение 700, ссылка на него записывается в uselessVar
            
            System.out.println(o.toString() + i + ii);  
            // 6 В куче создаётся объект класса String, и ссылка на него передастся в метод println(), для которого создастся новый фрейм
            
        }
    }


```
