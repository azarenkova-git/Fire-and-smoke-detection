# Fire and Smoke Detection using YOLOv8
Проект по автоматическому обнаружению огня и дыма с использованием модели YOLOv8. В качестве основной архитектуры используется YOLOv8m, а для повышения разнообразия тренировочного набора применяется аугментация изображений с использованием библиотеки Albumentations. Основные метрики – Recall, Precision и mAP – служат ключевыми индикаторами эффективности модели, позволяющими оценить её способность надежно обнаруживать огонь и дым в реальных условиях.

# Требования
- Python: 3.11 (или выше)
- PyTorch: 2.6.0+cu124
- Ultralytics YOLO: 8.3.107
- Albumentations: 1.0.0 или выше
- OpenCV: для загрузки и сохранения изображений

# Подготовка данных
Данные разделены на тренировочную и валидационную выборки.
Файлы аннотаций должны быть в формате YOLO: каждая строка содержит
class_id x_center y_center width height, где все значения нормализованы относительно размеров изображения.

Файл data_correct.yaml должен содержать пути к папкам с изображениями и информации о количестве классов и их именах.

# Аугментация данных
В проекте используется аугментация для увеличения числа тренировочных изображений. Основной пайплайн аугментаций реализован с помощью Albumentations и включает следующие преобразования:
- A.RandomBrightnessContrast: случайное изменение яркости и контраста.
- A.HueSaturationValue: изменение оттенка, насыщенности и значения.
- A.GaussianBlur: применение гауссова размытия.

Также реализована функция корректировки координат bounding box‑ов: координаты преобразуются из формата YOLO в уголовые, обрезаются до диапазона [0.0, 1.0] и затем возвращаются в исходный формат.

# Обучение модели
Обучение производится с использованием Ultralytics YOLO. В качестве эксперимента рассматривались модели YOLOn8s, YOLOn8n, YOLOn8m, YOLOn8l, YOLOn5s с различными гиперпараметрами. 

# Заключение
В итоговом эксперименте лучшими показателями по основным метрикам (Recall, Precision и mAP) продемонстрировала модель YOLOv8m. Модель была обучена с использованием следующих гиперпараметров: epochs=100, imgsz=640, batch=32,  optimizer="sgd", lr0=0.01.
