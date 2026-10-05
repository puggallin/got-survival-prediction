# Данные

Файлы данных в репозиторий не включены. Ноутбук скачивает их сам (ячейки `!gdown` в начале):

| Файл | Что это | Google Drive ID |
|---|---|---|
| `game_of_thrones_train.csv` | обучающая выборка (1557 строк, есть `isAlive`) | `1XL0VTygpZj-ZAuTNRBgApZTPQyNDnT-v` |
| `game_of_thrones_test.csv` | тестовая выборка (389 строк, без `isAlive`) | `1h99toeF7lZ2I3iJwehgKO-QQmDaOe_O3` |

Скачать вручную:

```bash
pip install gdown
gdown 1XL0VTygpZj-ZAuTNRBgApZTPQyNDnT-v   # train
gdown 1h99toeF7lZ2I3iJwehgKO-QQmDaOe_O3   # test
```

Источник исходных данных — [A Wiki of Ice and Fire](http://awoiaf.westeros.org/);
