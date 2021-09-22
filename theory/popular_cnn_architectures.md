# Популярные архитектуры CNNs

Существуют общепринятые, проверенные временем архитектуры свёрточных нейронных сетей, которые используют до сих пор. Самые примечательные из них - VGG, GoogLeNet и ResNet. В этих нейронных сетях используются методы, призванные решать проблему затухающего градиента - в глубоких, действительно глубоких, сетях значение градиента неизбежно стремится к нулю, из-за чего веса модели не обновляются и модель в итоге не обучается.

Рассмотрим архитектуры GoogLeNet и ResNet, а точнее - не самые сложные их вариации.


## GoogLeNet

### InceptionBlock

GoogLeNet состоит из последовательных свёрточных модулей, которые называются **InceptionBlock**. Возможно, мы хотим применить к входному тензору несколько параллельных операций, например свёртку (3, 3) и свёртку (5, 5), и посмотреть, что получится в каждом из вариантов. Эту идею и воплощает InceptionBlock.

![inception_block](https://raw.githubusercontent.com/TheDim0n/TensorFlow-Learning/master/images/inception_block.png)

> После каждой свёртки размер изображения сохраняется, а результаты соединяются (concatenate) по каналам.

Как же GoogLeNet решает проблему затухания градиента? Дело в том, что модель имеет 3 классификатора (один основной и два вспомогательных), следовательно функция потерь считается 3 раза. Градиент вычисляется от суммы значений всех функций потерь.


![inception_block](https://raw.githubusercontent.com/TheDim0n/TensorFlow-Learning/master/images/googlenet-architecture.png)


## ResNet

### ResidualBlock

Microsoft воплотил довольно простую, но очень эффективную идею.

Пусть *X* - входной тензор. Применим к нему какие-то операции и результат добавим к тензору *X*.

![residual_block](https://raw.githubusercontent.com/TheDim0n/TensorFlow-Learning/master/images/ResidualBlock.png)

> Проверьте самостоятельно, что теперь градиент заведомо точно отличен от нуля.

RenNet состоит из нескольких последовательных ResidualBlock (альтернативное название - ResNetBlock), количество которых доходит до 150. Отличительной особеннойстью ResNet является слой GlobalAveragePooling2D, благодаря которому в нейронную сеть можно передавать изображения любого размера (но обязательно RGB и желательно, чтобы высота и ширина нацело делились на 32).

![residual_block](https://raw.githubusercontent.com/TheDim0n/TensorFlow-Learning/master/images/ResNet.png)


## Комбинирование

И такое тоже может быть. И не только такое.

![InceptionResnetBlocks](https://raw.githubusercontent.com/TheDim0n/TensorFlow-Learning/master/images/InceptionResnetBlocks.png)