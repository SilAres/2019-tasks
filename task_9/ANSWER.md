# Ответ на вопрос №9

## Ответ предоставил Данил Тюлькин @Danil_Tyulkin, за что ему большое спасибо!

```
base64 -w 0 flag.txt | sed -r 's/(.{9})/\1#/g' | awk '{split($0,a,"#"); print a[4],a[2],a[3],a[1]}' | tr " " "%" | gzip -cf | base64 -w 0 | xxd -E
```


**Что делала такая команда по порядку:**
```
1. Брала содержимое flag.txt и кодировала её в base64

2. Добавляла # через каждые 9 символов

3. Разделяла строку на подстроки, разделённые символом "#", меняла местами 4 и 1 подстроки, 
   склеивала их обратно, на этот раз с " " между подстроками вместо "#"

4. Заменяла " " на "%"

5. Архивировала промежуточный результат

6. Повторно кодировала в base64

7. Выводила хексдамп полученной строки
```


 
**Что нам требуется сделать, чтобы восстановить flag.txt^:**
```

1. Преобразовать хексдамп в строку

2. Декодировать строку из base64

3. Разархивировать промежуточный результат

4. Разделить строку на подстроки, разделённые символом "%", 
   поменять местами 4 и 1 подстроки, склеить их обратно

5. Убрать " ", получившиеся в результате прошлого шага

6. Декодировать строку из base64
```


Как можно увидеть, делать обратные операции на каждый шаг необходимости нет.

Для нашей цели составим такую вот команду (hex.txt - файл с хексдампом):

```
xxd -r hex.txt | base64 -d | gunzip | awk '{split($0,a,"%"); print a[4],a[2],a[3],a[1]}' | tr -d " " | base64 -d > flag.txt
```
**Промежуточные значения:**
```
1.H4sIAORDfVwAAyv1NfQyCwg2tFQNMfQKcPFz9vNQ9cv3dTepCnFxUw3KrnAKqiow9+ECAF/KMlgoAAAA

2.?C}\ +?5?2

1?    6?T

p?s??P???u7?

?pS

?*0?? _?2X

(архив строки)

3.uM1J6PS19%T1JPDNCNH%NoMG4zTDF%RkxBRzp7L

4.RkxBRzp7L T1JPDNCNH NoMG4zTDF uM1J6PS19

5.RkxBRzp7LT1JPDNCNHNoMG4zTDFuM1J6PS19

6.FLAG:{-=I<3B4sh0n3L1n3Rz=-}
```