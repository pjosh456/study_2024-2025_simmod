---
## Front matter
lang: ru-RU
title: Лабораторная работа 5
subtitle:  Модель эпидемии (SIR)
author:
  - Алади П. Ч.
institute:
  - Российский университет дружбы народов, Москва, Россия

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
---

# Информация

## Докладчик

:::::::::::::: {.columns align=center}
::: {.column width="70%"}

  * Алади Принц Чисом
  * студент
  * Российский университет дружбы народов
  * [103225007@pfur.ru](mailto:1032225007@pfur.ru)
  * <https://pjosh456.github.io/>

:::
::: {.column width="25%"}

:::
::::::::::::::

## Цель работы

Построить модель SIR в *xcos* и OpenModelica.

## Задание

1. Реализовать модель SIR в в *xcos*;
2. Реализовать модель SIR с помощью блока Modelica в в *xcos*;
3. Реализовать модель SIR в OpenModelica;
4. Реализовать модель SIR с учётом процесса рождения / гибели особей в xcos (в том числе и с использованием блока Modelica), а также в OpenModelica;
5. Построить графики эпидемического порога при различных значениях параметров модели (в частности изменяя параметр $\mu$);
6. Сделать анализ полученных графиков в зависимости от выбранных значений параметров модели.

## Выполнение лабораторной работы

$$
\begin{cases}
  \dot s = - \beta s(t)i(t); \\
  \dot i = \beta s(t)i(t) - \nu i(t);\\
  \dot r = \nu i(t),
\end{cases}
$$

где $\beta$ -- скорость заражения, $\nu$ -- скорость выздоровления.

## Реализация модели в xcos

Зафиксируем начальные данные: $\beta = 1, \, \nu = 0,3, s(0) = 0,999, \, i(0) = 0,001, \, r(0) = 0.$

## Реализация модели в xcos

![Задание переменных окружения в xcos](image/1.jpg){#fig:001 width=70%}

## Реализация модели в xcos

![Модель SIR в xcos](image/2.jpg){#fig:002 width=70%}

## Реализация модели в xcos

![Задание начальных значений в блоках интегрирования](image/3.jpg){#fig:003 width=70%}

## Реализация модели в xcos

![Задание начальных значений в блоках интегрирования](image/4.jpg){#fig:004 width=70%}

## Реализация модели в xcos

![Задание конечного времени интегрирования в xcos](image/5.jpg){#fig:005 width=70%}

## Реализация модели в xcos

![Эпидемический порог модели SIR при $\beta = 1, \nu = 0.3$](image/6.jpg){#fig:006 width=70%}

## Реализация модели с помощью блока Modelica в xcos

![Модель SIR в xcos с применением блока Modelica](image/7.jpg){#fig:007 width=70%}

## Реализация модели с помощью блока Modelica в xcos

![Параметры блока Modelica для модели SIR](image/8.jpg){#fig:008 width=50%}

## Реализация модели с помощью блока Modelica в xcos

![Параметры блока Modelica для модели SIR](image/9.jpg){#fig:009 width=50%}

## Реализация модели с помощью блока Modelica в xcos

![Эпидемический порог модели SIR при $\beta = 1, \nu = 0.3$](image/10.jpg){#fig:010 width=70%}

## Упражнение

```
  parameter Real I_0 = 0.001;
  parameter Real R_0 = 0;
  parameter Real S_0 = 0.999;
  parameter Real beta = 1;
  parameter Real nu = 0.3;
  parameter Real mu = 0.5;
  Real s(start=S_0);
  Real i(start=I_0);
  Real r(start=R_0);
  
equation
  der(s)=-beta*s*i;
  der(i)=beta*s*i-nu*i;
  der(r)=nu*i;
```

## Упражнение

![Эпидемический порог модели SIR при $\beta = 1, \nu = 0.3$](image/11.jpg){#fig:012 width=70%}

## Задание для самостоятельного выполнения

$$
\begin{cases}
  \dot s = - \beta s(t)i(t) + \mu (N - s(t)); \\
  \dot i = \beta s(t)i(t) - \nu i(t) - \mu i(t);\\
  \dot r = \nu i(t) - \mu r(t),
\end{cases}
$$

где $\mu$ — константа, которая равна коэффициенту смертности и рождаемости.

## Задание для самостоятельного выполнения

![Модель SIR с учетом демографических процессов в xcos](image/13.jpg){#fig:013 width=60%}

## Задание для самостоятельного выполнения

![График модели SIR с учетом демографических процессов](image/14.jpg){#fig:014 width=70%}

## Задание для самостоятельного выполнения

![Модель SIR с учетом демографических процессов в xcos с применением блока Modelica](image/15.jpg){#fig:015 width=70%}

## Задание для самостоятельного выполнения

![Параметры блока Modelica для модели SIR с учетом демографических процессов](image/16.jpg){#fig:016 width=50%}

## Задание для самостоятельного выполнения

![Параметры блока Modelica для модели SIR с учетом демографических процессов](image/17.jpg){#fig:017 width=50%}

## Задание для самостоятельного выполнения

![График модели SIR с учетом демографических процессов](image/18.jpg){#fig:018 width=60%}

## Задание для самостоятельного выполнения

```
  parameter Real I_0 = 0.001;
  parameter Real R_0 = 0;
  parameter Real S_0 = 0.999;
  parameter Real beta = 1;
  parameter Real nu = 0.3;
  parameter Real mu = 0.5;
  Real s(start=S_0);
  Real i(start=I_0);
  Real r(start=R_0);
  
equation
  der(s)=-beta*s*i + mu*i + mu*r;
  der(i)=beta*s*i-nu*i - mu*i;
  der(r)=nu*i - mu*r;
```

## Задание для самостоятельного выполнения

![График модели SIR с учетом демографических процессов](image/19.jpg){#fig:019 width=70%}

## Задание для самостоятельного выполнения

 $\beta = 1$, $\nu = 0.3, \mu = 0.1$

![График модели SIR с учетом демографических процессов](image/19.jpg){#fig:020 width=70%}

## Задание для самостоятельного выполнения

$\mu = 0.3$

![График модели SIR с учетом демографических процессов](image/20.jpg){#fig:021 width=50%}

## Задание для самостоятельного выполнения

$\mu = 0.9$

![График модели SIR с учетом демографических процессов](image/21.jpg){#fig:022 width=50%}

## Задание для самостоятельного выполнения

$\beta = 1$, $\nu = 0.1, \mu = 0.1$

![График модели SIR с учетом демографических процессов](image/22.jpg){#fig:023 width=50%}

## Задание для самостоятельного выполнения

$\mu = 0.9$

![График модели SIR с учетом демографических процессов](image/23.jpg){#fig:024 width=50%}

## Задание для самостоятельного выполнения

$\beta = 4$, $\nu = 0.3, \mu = 0.2$

![График модели SIR с учетом демографических процессов](image/24.jpg){#fig:025 width=50%}

## Выводы

В процессе выполнения данной лабораторной работы была построен модель SIR в *xcos* и OpenModelica.
