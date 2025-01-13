# Оценка параметров распределения

## 1. Несмещенность оценки
Рассмотрим случайную величину $K = \sum_{i=1}^{n} I(x - x_{i})$, где $I(x - x_{i})$ — индикаторная функция. Вероятность того, что $I(x - x_{i}) = 1$, равна:
$$ P(I(x - x_{i}) = 1) = P(x_{i} \leq x) = F(x)$$
Распределение случайной величины $K$ имеет следующие характеристики:
- Математическое ожидание:

$$M[K] = n p = n F(x)$$

- Дисперсия:

$$D[K] = n p (1 - p) = n F(x) (1 - F(x))$$

Оценка функции распределения $\hat{F}(x)$ имеет следующие свойства:
- Математическое ожидание:

$$M[\hat{F}(x)] = \frac{1}{n} M[K] = F(x) \quad \text{(несмещенность)}$$

- Дисперсия:

$$D[\hat{F}(x)] = \frac{1}{n} F(x) (1 - F(x))$$

Дисперсия достигает максимума при $F(x) = \frac{1}{2}$:

$$D[\hat{F}(x)] = \frac{0.25}{n}$$

Это соответствует медиане распределения.

## 2. Эффективность оценки
Оценка должна обладать минимальным рассеянием:

$$\hat{D}(\theta) = M[(\hat{\theta} - \theta)^2] = \min$$

Если оценка несмещенная, то это означает минимум дисперсии асимптотически. Эффективность при $n \to \infty$ определяется среднеквадратичным отклонением (СКО):

$$\sqrt{\hat{D}(\theta)} = \sqrt{M[(\hat{\theta} - \theta)^2]}$$

Какую оценку предпочесть:
- Несмещенную, но с большей дисперсией
- Смещенную с меньшей дисперсией

Смещение приемлемо до тех пор, пока оно мало по сравнению с СКО. Однако при суммировании нескольких независимых оценок смещение остается постоянным, а составляющая СКО, обусловленная дисперсией, уменьшается как $\frac{1}{\sqrt{n}}$. Таким образом, СКО полностью определяется смещением.

### Пример для нормального распределения
Для нормального распределения с неизвестным средним:

$$S^2 = \frac{1}{n} \sum_{i=1}^{n} (x_{i} - \overline{x})^2 $$

Дисперсия оценки:

$$\hat{D}(S^2) = \frac{2n - 1}{n^2} \sigma^4$$

Эта дисперсия меньше дисперсии несмещенной оценки:

$$S^2_{i} = \frac{1}{n - 1} \sum_{i=1}^{n} (x_{i} - \overline{x})^2$$

Дисперсия несмещенной оценки:
$$\hat{D}(S^2_{i}) = \frac{2}{n - 1} \sigma^4$$

## 3. Достаточность статистики

Некоторые статистические модели позволяют заменить выборку $X = (x_{1}, \dots, x_{n})$ на статистику $T(x)$, которая эквивалентна всей выборке при оценивании параметра$\theta$. Это позволяет сжать информацию до некоторой функции от выборки.

### Схема Бернулли

Рассмотрим схему Бернулли:

$$P(X_{i} = x_{i}) = \theta^{x_{i}} (1 - \theta)^{1 - x_{i}}, \quad x_{i} \in \{0, 1\}$$

Совместное распределение выборки:

$$P\left( \prod_{i=1}^{n} X_{i} = x_{i} \right) = \prod P(X_{i} = x_{i}) = \prod \theta^{x_{i}} (1 - \theta)^{1 - x_{i}} = \theta^{\sum x_{i}} (1 - \theta)^{\sum (1 - x_{i})} = \theta^t (1 - \theta)^{n - t}$$

где $t = T(x) = \sum_{i=1}^n X_{i}$.

Условное распределение выборки$X$при условии $T(x) = t$ не зависит от $\theta$:

$$ P(X = x | T(x) = t) = \frac{\theta^t (1 - \theta)^{n - t}}{C_{n}^{t} \theta^{t} (1 - \theta)^{n - t}} = \frac{1}{C_{n}^t}$$

### Критерий факторизации

Векторная статистика $T$ в дискретной модели является достаточной тогда и только тогда, когда существуют функции $g$ и $h$, такие что:

$$ f(x, \theta) = g(T(x), \theta) h(x)$$

где $f(x, \theta)$ — совместная вероятность выборки.

Для схемы Бернулли:

$$ g(t, \theta) = \theta^t (1 - \theta)^{n - t}; \quad h(x) = 1; \quad t = \sum x_{i}$$

Для непрерывных моделей $f(x, \theta)$ — совместная плотность выборки. Достаточная статистика существует, если плотность может быть факторизована в виде:

$$f(x, \theta) = g(T(x), \theta) h(x)$$

## 4. Неравенство Рао-Крамера

Для несмещенных оценок и оценок с постоянным смещением дисперсия оценки удовлетворяет неравенству:

$$ D_{\theta}[\hat{\theta}] \geq \frac{1}{M\left( \frac{d}{d\theta} \ln L(\theta, x) \right)^2}$$

где $L(\theta, x) = f(x | \theta)$ — функция правдоподобия. Знак равенства достигается только для **эффективных оценок**.

### Пример

Для нормального распределения $x_{i} \sim N(\theta, \sigma^2)$ оценка $\overline{x}$ с дисперсией $\frac{\sigma^2}{n}$ является эффективной.

### Контрпример

Для равномерного распределения на $[0, \theta]$ оценка $X_{(n)}$ (максимум выборки) имеет точность порядка $\frac{1}{n}$, что является сверхэффективной оценкой.

### Условия равенства в неравенстве Рао-Крамера

Неравенство Рао-Крамера обращается в равенство, если:

$$ \frac{d}{d\theta} \ln L(\theta, x) = \eta(\theta) (\hat{\theta} - \theta)$$

Это выражение не зависит от $\hat{\theta}$ и выборки, если $\hat{\theta}$ является достаточной статистикой.

### Критерий существования несмещенной эффективной оценки

1. Достаточность статистики.
2. Выполнение условия равенства в неравенстве Рао-Крамера.

### Информационное количество Фишера

Информационное количество Фишера определяется как:

$$I_{n}(\theta) = M\left[ \left( \frac{d}{d\theta} \ln L(\theta, x) \right)^2 \right] = -M\left[ \frac{d^2}{d\theta^2} \ln L(\theta, x) \right]$$

Это среднее количество информации об оцениваемом параметре, содержащейся в выборке. Дисперсия эффективной оценки:

$$D_{ef}(\theta) = \frac{1}{I_{n}} = \frac{1}{n I_{1}(\theta)}$$

## Методы оценивания параметров

1. **Графический метод**  
   Используется для грубого определения оценок. Подходит для моделей сдвиг-масштаба. С помощью линейной аппроксимации можно получить оценки параметров сдвига и масштаба.

2. **Метод моментов (ММ)**  
   Оценки параметров находятся путем приравнивания выборочных моментов к теоретическим.

3. **Метод максимального правдоподобия (ММП)**  
   Оценки параметров находятся путем максимизации функции правдоподобия.

### Подробнее о графическом методе

Вероятностная бумага позволяет представить теоретическую функцию распределения в виде прямой:

$$F^{-1}(F(x)) = x \quad \text{(квантиль распределения)}$$

По оси $x$ откладываются выборочные значения, а по оси $F^{-1}(\hat{F}(x_i))$ — соответствующие квантили.