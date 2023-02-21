# Мониторинг работы JvmExperience в программе VisualVM

## Описание программы
До старта основной части программы проходит 30 с. При вызове метода loadToMetaspaceAllFrom(String packageName) в метаспейс мемори загружаются все классы из данной библиотеки. Их имена сохраняются во множестве «allClasses». Метод вызывается 3 раза с паузами между вызовами по 3 с.
Далее создаются объекты типа SimpleObject. Для этого используется метод createSimpleObjects(int count). Метод вызывается 3 раза с паузами между вызовами по  3 с.

## Работа с VisualVM
Ниже на графиках нанесены пояснения и логи из консоли IIDEA. На графиках памяти видна динамика уменьшения/увеличения (занятой и доступной) хип мемори, а также увеличения метаспейс мемори. Также видно, что условно вся нагрузка на процессор возникает за счет работы приложения. GC почти не нагружает процессор. Сборка мусора заметно видна на графике кучи только один раз (видимо после того, как работа с объектами методов loadToMetaspaceAllFrom() закончилась и ссылки на эти объекты отсутствуют). Также во время второго вызова метода createSimpleObjects() видно сначала медленное заполнение кучи, а потом заполнение происходит более быстро. В этом же интервале по времени была еще одна сборка мусора. При других вызовах GC на графике кучи уменьшение памяти явно не наблюдается.

![1](https://github.com/AlekseyBel0v/4.10._task2_VisualJM/blob/main/images/classes.jpg?raw=true)

![2](https://github.com/AlekseyBel0v/4.10._task2_VisualJM/blob/main/images/cpu.jpeg?raw=true)

![3](https://github.com/AlekseyBel0v/4.10._task2_VisualJM/blob/main/images/heap%20memory.jpg?raw=true)

![4](https://github.com/AlekseyBel0v/4.10._task2_VisualJM/blob/main/images/metaspace%20memory.jpg?raw=true)

![5](https://github.com/AlekseyBel0v/4.10._task2_VisualJM/blob/main/images/threads.jpg?raw=true)