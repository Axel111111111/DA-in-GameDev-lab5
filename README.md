# DA-in-GameDev-lab5
АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #5

Интеграция экономической системы в проект Unity и обучение ML-Agent.

Выполнил:
- Зубов Алексей Иванович
- РИ-210946 
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 80 |
| Задание 2 | * | 20 |


знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨


Цель работы
Научиться интегрировать экономическую систему в проект Unity и обучать ML-Agent.

## Задание 1
## Измените параметры файла. yaml-агента и определить какие параметры и как влияют на обучение модели.

В начале лабораторной работы я открыл проект Unity и подробно ознакомился с объектами на сцене и с его работой.

 ![изначальный проект](https://user-images.githubusercontent.com/49406824/205310370-c03c1754-1a50-41f5-9ae9-096d21a5f95e.png)

Далее добавил Economic.yaml в папку с проектом. Содержимое файла Economic.yaml:

    behaviors:
      Economic:
        trainer_type: ppo
        hyperparameters:
          batch_size: 1024
          buffer_size: 10240
          learning_rate: 3.0e-4
          learning_rate_schedule: linear
          beta: 1.0e-2
          epsilon: 0.2
          lambd: 0.95
          num_epoch: 3      
        network_settings:
          normalize: false
          hidden_units: 128
          num_layers: 2
        reward_signals:
          extrinsic:
            gamma: 0.99
            strength: 1.0
        checkpoint_interval: 500000
        max_steps: 750000
        time_horizon: 64
        summary_freq: 5000
        self_play:
          save_steps: 20000
          team_change: 100000
          swap_steps: 10000
          play_against_latest_model_ratio: 0.5
          window: 10

После чего активировал виртуальное пространство и запустил обучение MLAgent через Anaconda Prompt

![запуск обучения](https://user-images.githubusercontent.com/49406824/205312117-3a0d3e0b-f5bf-4954-811d-b40c0aac1947.png)

![результат после запуска обучения](https://user-images.githubusercontent.com/49406824/205312137-97c7076e-c952-4698-ab25-cfdea634e9a8.png)

Потом я установил TensorBoard, чтобы была возможность построения графиков для оценки результатов обучения.
Запустил TensorBoard и открыл вкладку с графиками

![TensorBoard1](https://user-images.githubusercontent.com/49406824/205313280-106d56fb-8212-43e2-a13d-f85f1ba23003.png)

![TensorBoard2](https://user-images.githubusercontent.com/49406824/205313312-30da1a35-e3db-4fee-85a3-b093224c52cb.png)


## Задание 2
## Опишите результаты, выведенные в TensorBoard.

### Environment
Cumulative Reward - вознагрaждение зa эпизод для всeх агентов. Увеличивается, когда эпизод обучения успeшен. Постоянно увеличивaется.

Episode Length - продолжительность эпизода обучения в среде для агентов.

### Losses
Policy Loss - величина функции потери политики, где политика - процесс принятия решений. Во время успешного эпизода график идёт вниз.

Value Loss - потеря функции значения. Она моделирует, насколько хорошо агент прогнозирует значение своего следующего состояния. Должна увеличиваться, пока агент обучается, а затем уменьшаться, когда вознаграждение стабилизируется.

### Policy
Entropy - график случайности решений модели. Во время успешного эпизода график идёт вниз.

Beta - гиперпараметр для настройки Entropy.

Epsilon - гиперпараметр, влияет на скорость развития политики.

Extrinsic Reward - соответствует среднему совокупному вознаграждению, полученному от окружающей среды за эпизод.

Value Estimate - это среднее значение, посещённое всеми состояниями агента. 

Learning Rate - показывает величину шага при поиске оптимальной политики.  Линейно уменьшается.

Self play
ELO - показывает силу сети.

## Выводы

В этой лабораторной я научился интегрировать экономическую систему в проект Unity, используя мл агента. Научился выводить графики в TensorBoard и анализировать их.
num_epoch увеличил. Определяет количество проходов через буфер опыта при выполнении оптимизации градиентного спуска.
normalize поставил true. Определяет применяется ли нормализация к входным данным векторных наблюдений.
hidden_units Определяет количество единиц в каждом полносвязном слое нейронной сети. По сути не сильно влияет на обучение.
num_layers Определяет количество скрытых слоев в нейронной сети. Мало влияет на обучение.
gamma Этот параметр можно рассматривать как то, как далеко в будущем агент должен заботиться о возможных вознаграждениях.
strength Коэффициент, на который умножается вознаграждение, данное средой.

**BigDigital Team: Denisov | Fadeev | Panov**
