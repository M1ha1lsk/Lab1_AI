# Лабораторная работа 1 (Киберфизические системы, CV)

## Автор

- ФИО: Калюжный Михаил Сергеевич
- Группа: М8О-408Б-22

## Датасет

- Название: Ships in Aerial Images
- Ссылка: [https://www.kaggle.com/datasets/siddharthkumarsah/ships-in-aerial-images](https://www.kaggle.com/datasets/siddharthkumarsah/ships-in-aerial-images)

## Обоснование выбора датасета

Датасет содержит около 26.9k аэрофотоснимков с разметкой bounding boxes в формате YOLO для одного класса (`ship`). Это подходит для задачи обнаружения объектов и позволяет сосредоточиться на качестве детекции без дополнительной сложности мультиклассовой постановки.

Практическая значимость задачи: обнаружение судов используется в морской безопасности, контроле рыболовства, мониторинге загрязнений, а также в задачах обороны и охраны морских границ.

## Структура решения

- Основной ноутбук: `lab1_cp.ipynb`
- Используемый фреймворк для детекции: `ultralytics` (YOLOv11)
- Дополнительно реализована собственная lightweight-модель детекции (пункт 4 задания)

## Воспроизводимая инструкция: установка и запуск

### 1) Подготовка окружения

В корне папки:

```bash
python -m venv .venv
```

Активация:

- Windows (PowerShell):
```bash
.venv\Scripts\Activate.ps1
```
- Linux/macOS:
```bash
source .venv/bin/activate
```

Установка зависимостей:

```bash
pip install --upgrade pip
pip install torch torchvision ultralytics opencv-python matplotlib pandas tqdm jupyter
```

### 3) Подготовка данных

1. Скачайте архив датасета с Kaggle по ссылке выше.
2. Поместите файл `ships-aerial-images.zip` в папку:
   - `./data/`
3. В ноутбуке предусмотрена автоматическая распаковка архива в:
   - `./data/ships-aerial-images/`

Ожидаемая структура после распаковки:

```text
data/
  ships-aerial-images.zip
  ships-aerial-images/
    train/
      images/
      labels/
    valid/
      images/
      labels/
    test/
      images/
      labels/
```

### 4) Запуск

```bash
jupyter notebook
```

Откройте файл:

- `lab1_cp.ipynb`

И выполните ячейки сверху вниз:

1. Подготовка путей, данных и `data.yaml`
2. Обучение и оценка YOLOv11 baseline
3. Обучение и оценка YOLOv11 improved baseline
4. Обучение и оценка собственной модели (базовая и improved-конфигурация)
5. Финальная сравнительная таблица метрик

### 5) Артефакты после запуска

- Веса и логи YOLO: `./runs/detect/...`
- Графики и веса кастомной модели: `./results/...`

## Метрики качества

В работе используются:

- `mAP50`
- `mAP50-95`
- `Precision`
- `Recall`
- `F1`

Эти метрики позволяют оценить и точность локализации, и баланс между ложными срабатываниями и пропусками.
