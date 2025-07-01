Link dos vídeos: https://drive.google.com/drive/folders/17NPiLodnsyGCmYuaX3jTUlHYftfHdsq_?usp=sharing

# 🧠 Detecção de Objetos com YOLOv8

Este projeto utiliza o modelo **YOLOv8m** (Ultralytics) para treinar e validar um detector de objetos com base em um conjunto de dados personalizado contendo 10 classes.

## 📁 Dataset

O dataset foi extraído do arquivo `deteccaodeobjetos.zip` e estruturado no formato YOLO, com diretórios de `train/` e `valid/` organizados em:

meu_dataset/
├── train/
│ ├── images/
│ └── labels/
├── valid/
│ ├── images/
│ └── labels/
└── data.yaml

markdown
Copiar
Editar

As 10 classes utilizadas foram:

- `door`
- `cabinetDoor`
- `refrigeratorDoor`
- `window`
- `chair`
- `table`
- `cabinet`
- `couch`
- `openedDoor`
- `pole`

## ⚙️ Treinamento

O modelo foi treinado com o seguinte código:

```python
from ultralytics import YOLO

model = YOLO("yolov8m.pt")
model.train(
    data="data.yaml",
    epochs=15,
    imgsz=640,
    batch=8,
    name="treino_yolov8m"
)
O processo foi realizado no Google Colab com suporte a GPU (CUDA).

📊 Validação
Para validar o modelo e obter métricas:

python
Copiar
Editar
model = YOLO("runs/detect/treino_yolov8m/weights/last.pt")
metrics = model.val()
As métricas geradas incluem:

Curva PR (precisão vs. revocação)

Curva F1-score

Matriz de confusão

mAP@0.5

📦 Resultados
Os resultados das predições e métricas visuais são salvos automaticamente em:

bash
Copiar
Editar
runs/detect/treino_yolov8m/
Incluindo:

PR_curve.png

F1_curve.png

confusion_matrix.png

Imagens com predições e rótulos

🧪 Inferência
Para realizar inferência em novas imagens:

python
Copiar
Editar
model = YOLO("runs/detect/treino_yolov8m/weights/best.pt")
results = model("path/para/imagem.jpg")
results.show()
📌 Observações
Projeto desenvolvido como parte de um trabalho técnico.
O link dos videos está nesse arquivo, e no relatório técnico.
O modelo pode ser aprimorado com mais dados, ajustes de hiperparâmetros ou técnicas de aumento de dados (data augmentation).
