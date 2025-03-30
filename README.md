## Language-Classification-CNN-

El presente repositorio contiene la metodología que fue utilizada para entrenar un modelo de clasificación de imágenes con el fin de clasificar lenguas (específicamente español y maya en este caso), esta metodología incluye la decisión de usar una clasificación con imágenes, la recolección de audios, así como el código relevante para manejo de audios y el entrenamiento

## Clasificación con imágenes
El entrenamiento se hizo con las imágenes de los espectogramas extraídas de los audios, se usaron los espectogramas debido a que con ellos no es necesaria la anotación o transcripción de los audios, y que existen trabajos previos que utilizaron esta característica de los audios [1].

## Recolección de audios
Los audios utilizados para el entrenamiento se encuentran en las carpetas "Spanish" y "Mayan", sin embargo, debido a que uno de los corpus utilizados no es público, no contienen la totalidad de los audios. Los audios de dominio público se consiguieron de las siguientes fuentes:
# Español
Ciempiess-Balanced [2]
# Maya
T'aantsil [3]
DoReCo [4]

Para ambas lenguas, los audios se mantuvieron con una duración entre 3 y 15 segundos, para esto, algunos audios de T'aantsil y DoReCo fueron divididos en dos o más audios, esta división se realizó con el código encontrado en el archivo "split_audios.py"


# Entrenamiento del modelo
El archivo "Audio Classification (CNN).ipynb" encontrado en el repositorio contiene todo el código necesario para realizar el entrenamiento una vez recolectados los audios, los contenidos de la libreta contienen una adaptación y algunas funciones adicionales a la encontrada en https://github.com/jeffprosise/Deep-Learning/blob/master/Audio%20Classification%20(CNN).ipynb [5]

Aunque en el archivo "Audio Classification (CNN).ipynb" el procedimiento es para solo un modelo, se realizaron tres entrenamientos usando un modelo base para cada uno, el modelo base actual se puede conocer observando el siguiente fragmento de código:

from tensorflow.keras.applications import MobileNetV2
from tensorflow.keras.applications.mobilenet import preprocess_input

base_model = MobileNetV2(weights='imagenet', include_top=False, input_shape=(224, 224, 3))

En ese fragmento se está utilizando MobileNetV2 como modelo base, los otros dos modelos base usados fueron ResNet50 y ResNet152, para poder realizar el entrenamiento con estos modelos base, se debe reemplazar el fragmento de código anterior con alguno de los siguientes (dependiendo del modelo base a usar):

from tensorflow.keras.applications import ResNet50
from tensorflow.keras.applications.resnet import preprocess_input

base_model = ResNet50(weights='imagenet', include_top=False, input_shape=(224, 224, 3))

from tensorflow.keras.applications import ResNet152
from tensorflow.keras.applications.resnet import preprocess_input

base_model = ResNet152(weights='imagenet', include_top=False, input_shape=(224, 224, 3))

# Referencias
[1] Mukherjee, H., Ghosh, S., Sen, S., Sk Md, O., Santosh, K. C., Phadikar, S., & Roy, K. (2019). Deep learning for spoken language identification: Can we visualize speech signal patterns?. Neural Computing and Applications, 31, 8483-8501. 
[2] Ciempiess-unam. Recuperado de https://ciempiess.org/downloads 
[3] T’aantsil. Recuperado de https://taantsil.com.mx/ 
[4] Skopeteas, Stavros, Amedee Colli Colli, Daniela Schellenbach, Carolin Brokmann, Florian Fischer and Maya Gálvez Wimmelmann. 2024. Yucatec Maya DoReCo dataset. In Seifart, Frank, Ludger Paschen and Matthew Stave (eds.). Language Documentation Reference Corpus (DoReCo) 2.0. Lyon: Laboratoire Dynamique Du Langage (UMR5596, CNRS & Université Lyon 2). (https://doi.org/10.34847/nkl.9cbb3619). 
[5] Jeff Prosise (2021). Deep-Learning [Software]. GitHub. https://github.com/jeffprosise/Deep-Learning/blob/master/Audio%20Classification%20(CNN).ipynb 