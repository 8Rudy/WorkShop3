# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #1 выполнил(а):
- Чернявская София Владиславовна
- РИ230932
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

## Цель работы
Научиться работать с балансировкой оружия в игре 

## Задание 1
### Расширьте варианты доступного оружия в игре.
Ход работы:
Решить какое оружие необходимо для расширения вариативности выбора в игре Save RTF и сбалансировать его, используя гугл таблицу

Для данной работы я выбрала копье, лук, арбалет, миномет и огнемет

Ссылка на заполненую по шаблону гугл таблицу
https://docs.google.com/spreadsheets/d/12V0QD20hEG96FhofnroFfmMycMuCZ-Wvk7E-xRa7ONo/edit?gid=0#gid=0

## Задание 2
### Визуализируйте параметры оружия в таблице. Постройте примеры для следующих математических величин:
- Среднеквадратическое отклонение (СКО)
- Разброс урона оружия
- Вариативность времени отклика игрока (реакция на события)

![d4fb2be8-c6ee-4fbd-aaa3-ceb0b92a7c6d](https://github.com/user-attachments/assets/4998665e-2750-49d0-bec1-b793b0ce3cb0)




## Задание 3
### визуализировать данные из google-таблицы с помощью Python 
```py
import numpy as np
import matplotlib.pyplot as plt
import random as rnd

def simulate_shots(weapon_name, num_shots, damage_per_shot, hit_probabilities, ax):
    # Генерация случайных выстрелов с отклонениями
    np.random.seed(rnd.randint(32, 64))
    shots_coords = np.random.normal(loc=0, scale=5, size=(num_shots, 2))

    # Вычисляем отклонения (расстояния от центра цели)
    distances = np.linalg.norm(shots_coords, axis=1)

    # Проверяем попадания
    hits, misses = [], []
    for i, distance in enumerate(distances):
        distance_index = min(int(distance), len(hit_probabilities) - 1)
        hit_chance = hit_probabilities[distance_index] / 100
        if np.random.rand() < hit_chance:
            hits.append(shots_coords[i])
        else:
            misses.append(shots_coords[i])

    hits = np.array(hits)
    misses = np.array(misses)

    # Выводим результаты
    print(f"{weapon_name}: {len(hits)} попаданий из {num_shots}")
    print(f"СКО отклонений: {np.std(distances):.2f} пикселей")

    # Визуализация
    if len(hits) > 0:
        ax.scatter(hits[:, 0], hits[:, 1], color='green', label='Попадания')
    if len(misses) > 0:
        ax.scatter(misses[:, 0], misses[:, 1], color='red', label='Промахи')
    ax.scatter(0, 0, color='blue', s=100, label='Цель')
    ax.set_xlim(-20, 20)
    ax.set_ylim(-20, 20)
    ax.axhline(0, color='black', lw=0.5)
    ax.axvline(0, color='black', lw=0.5)
    ax.set_title(f"{weapon_name}\nУрон за выстрел: {damage_per_shot}")
    ax.legend()
    ax.set_aspect('equal', adjustable='box')

# Параметры для различных оружий
weapons = [
    ("Копье", 10, 4, [100.00, 83.33, 83.33, 66.67, 66.67, 50.50, 33.33, 33.33, 00.00]),
    ("Лук", 50, 4, [16.67, 33.33, 33.33, 66.67, 66.67, 66.67, 66.67, 66.67, 83.33, 83.33]),
    ("Огнемет", 20, 4, [83.33, 66.67, 50.00, 50.00, 33.33, 16.67, 16.67]),
    ("Миномет", 15, 8, [16.67, 16.67, 33.33, 33.33, 33.33, 50.00, 66.67, 50.00, 83.33, 100.00, 100.00]),
    ("Арбалет", 30, 3, [66.67, 66.67, 66.67, 50.00, 50.00, 50.00, 33.33, 33.33])
]

# Создаем фигуру и подграфики
fig, axs = plt.subplots(2, 2, figsize=(12, 12))
axs = axs.flatten()  # Преобразуем 2D массив в 1D для простоты использования

# Запускаем симуляцию для каждого оружия
for i, weapon in enumerate(weapons):
    simulate_shots(*weapon, axs[i])

plt.tight_layout()  # Упаковываем подграфики
plt.show()

```

## Выводы

Я научилась работать с балансом, эта практика была одной из самых интересныхдля меня, так как пришлось продумывать какие параметры надо задать оружию, что бы оно соответствовало описанию и при этом находилось в разумных рамках 

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
