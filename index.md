---
title: Instrucciones del ejercicio
permalink: index.html
layout: home
---

# Ejercicios

En esta página se enumeran los ejercicios asociados con el contenido de aptitudes de Microsoft en [Microsoft Learn.](https://learn.microsoft.com)

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %} {% for activity in labs  %}
- [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }}) {% endfor %}

