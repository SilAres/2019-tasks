# Ответ на вопрос №5

## Вариант от Павла Шлюндина @Riocool

```
(\d+\.\d+\.\d+\.\d+?) - - \[(.+?)\]\s*\"\w*\s*\/.*?(?=\?)(?:(?:\&|\?)([\w\%]*?)\=(.+?(?:or|1\=1|script|select|union|alert|sleep).+?(?=(?:\?|\&| HTTP))))*
```

## Другой вариант

Для написания регулярных выражений, люблю https://regex101.com

_P.S. Плюс от себя добавил именование групп **?<NAME_GROUP>** в задание это не требуется_

```
/(?<IP>\d+\.\d+\.\d+\.\d+?).*\[(?<DATE>.*)\].*\/\?(?<NAME>.*)=(?<PARAMS>.*(?:or|1=1|script|select|union|alert|sleep).*) HTTP/gmU
```

Если не указать модификатор _**U**_ в группе **IP** будет обрезать до 1 символа, окончание.