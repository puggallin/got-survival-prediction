# Game of Thrones: выживет ли персонаж?


**Стек:** Python, pandas, NumPy, matplotlib, seaborn, scikit-learn.

## Структура репозитория

```
├── notebooks/GOT_deadoralive.ipynb   # решение (предобработка, модели, предсказание)
├── data/                             # см. data/README.md — откуда берутся данные
├── requirements.txt
└── README.md
```

## Результаты

Метрика — accuracy. Валидация: 20% обучающей выборки (`random_state=42`).
Для ориентира: доля живых в train — 0.7784, то есть модель «все живы» дала бы примерно такую accuracy.

| Модель | Accuracy (val) |
|---|---|
| `RandomForestClassifier(random_state=42)` | 0.8237 |
| `LogisticRegression(max_iter=1000)` | 0.7724 |

Пример из задания 2.2 (`LogisticRegression()` с параметрами по умолчанию): 0.7756.

Лучшая модель — `RandomForestClassifier`. Для итогового предсказания она переобучена на всей обучающей выборке. Accuracy на скрытом тесте (проверка на Stepik): **0.7326**.

## Предобработка признаков

- `age` → `age_value` (NaN → 0) + флаг `age_no_data`
- `numDeadRelations` → бинарный `boolDeadRelations`
- `culture` → 11 укрупнённых групп по словарю из задания, пропуски → `culture_no_data`
- `title`, `house` → 25 самых частых значений + `other` / `no_data`
- `isAliveSpouse`, `isAliveFather`, `isAliveHeir` → значение + флаг `_no_data`; `isAliveMother` → только флаг `_no_data`
- `mother`, `father`, `heir`, `spouse` → `no_data` / `known` / `targaryen`
- категориальные признаки → one-hot (`pd.get_dummies`, `drop_first=True`)
- `name` и `dateOfBirth` исключены
- тестовая выборка обрабатывается теми же словарями и списками «топ-25», что посчитаны на train, а столбцы выравниваются через `reindex(columns=X.columns, fill_value=0)`
- в тесте исправлены две строки с некорректным возрастом (S.No 1685 и 1869), как предложено в задании

## Запуск

Ноутбук разрабатывался в Google Colab: данные скачиваются ячейками `!gdown ...` в начале.

Локально:

```bash
pip install -r requirements.txt
jupyter notebook notebooks/GOT_deadoralive.ipynb
```
