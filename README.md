# Классификатор рецептов

*Work in progress*

Простое приложение, позволяющее подобрать теги к тексту рецепту (супы, говядина, зелень и т.д.)

Проект состоит из 3 частей - ML, Back и Front. Фронт и бэк живут как отдельные приложения на heroku.

## ML
Мультилейбл-классификатор, натренированный на датасете [Food.com](https://www.kaggle.com/shuyangli94/food-com-recipes-and-user-interactions). Тексты датасета - на английском, названия классов - вручную переведены на русский.

Под капотом классификатора - tfidf и логрег. 

## Back
Фласковое приложение с одной ручкой `/predict`, которая получает текст рецепта в теле POST-запроса:
```json
{"input":"Готовим борщ"}
```
После получения запроса, приложение отправляет русский текст в API Я.Переводчика, получает английский текст, проводит предобработку текста,
классифицирует и отдает результат в формате:
```json
{"response": ["Бульоны и супы", "русская кухня"]}
```

## Front
Синглпейдж на Vue. Текстовое поле для ввода рецепта и кнопка "Подобрать теги", которая ходит на бэк с введенным текстом:

![](front-new.png)
