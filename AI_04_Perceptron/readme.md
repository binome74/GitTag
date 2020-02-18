Распознавание формата файла по содержимому с помощью простейшей искусственной нейронной сети
--------------------------------------------------------------------------------------------
Построена нейронная сеть из одного нейрона с 256 входами, определяющая типа файла по его содержимому: «PDF» или «не PDF». 

Для обучения сети следует заготовить около 40 файлов в формате «pdf» и около 40 файлов не в формате «pdf» и указать пути к ним в файлах ListNonPDF.txt и ListPDF.txt. Обрабатывая заготовленные файлы программа формирует входные векторы: набор вероятностей появления в файле того или иного символа. Обучение нейрона сводится к циклическому выполнению следующих действий:
1. Найти сумму произведений элементов входных векторов на элементы весового вектора:
2. Сравнить полученное значение с 0. Если значение больше 0, то подать на выход нейрона 1 (PDF), иначе – подать -1 ("не PDF").
3. Если на выходе нейрона получилось значение, которое должно получиться, то ничего не делать и перейти к рассмотрению следующего вектора.
4. Если на выходе нейрона получилось значение 1, а должно было получиться -1, то элементы вектора весовых коэффициентов (w) следует уменьшить(wi = wi - 2сxi)
5. Если на выходе нейрона получилось значение -1, а должно было получиться 1, то элементы вектора весовых коэффициентов (w) следует увеличить(wi = wi + 2сxi)
Подобная последовательность действий выполняется с данными ото всех входных файлов вперемешку до тех пор, пока примерно в 90-95% случаев получаемый выход нейрона будет совпадать с желаемым. Значение «с» в приведённой выше формуле – коэффициент скорости обучения, принят 0.2.
После того как сеть обучена, полученные коэффициенты сохраняются и можно попробовать с их помощью определять тип файлов, которые не участвовали в процессе обучения. Примерно в 90% случаев результат определения правильный.