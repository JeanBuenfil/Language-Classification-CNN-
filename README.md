# Language-Classification-CNN-

This repository contains the methodology employed to train a image classification model, with the goal of language classification (specifically mexican spanish and mayan).
This methodology includes deciding the use of image classification, getting the audios and relevant code for audio management and training

# Image classification

The training was done using the spectograms images extracted from the audios, the reason why spectrograms were used is because working with them it means there is no need for annotations or transcriptions, and previous works using this characteristic exist [1].

# Audio files
The audios used in the training can be found in the "Spanish" and "Mayan" folders, however, due to permission issues, not all of the audios are included.
The public domain audios can be found in the following sources:

## Mexican Spanish
Ciempiess-Balance (https://mega.nz/folder/k0QTyA6C#iRwTHwEqjYdlOlAVbMSFKw) [2].  
The CIEMPIESS BALANCE is a Radio Corpus designed to create acoustic models for automatic speech recognition and it is made up by recordings of spontaneous conversations in Mexican Spanish between a radio moderator and his guests. 
The CB is made up by 8555 audio files with transcripts. 2447 of those files (28.6%) come from male speakers and 6108 files (71.39%) come from female speakers.
1317 audio files were selected at random from the original 8555 while trying to keep a balance between male and female speakers, resulting in 778 audio files with female speakers and 539 audio files from male speakers. 

## Maya
T'aantsil [3]


Yucatec Maya DoReCo (https://sharedocs.huma-num.fr/wl/?id=OEm80dNUe88cfpejRnhmFE5IIFeGdCp9) [4]. 
The Yucatec Maya DoReCo dataset was compiled by Stavros Skopeteas in 2015 and further processed for DoReCo by Alejandra Camelo Cruz, Ludger Paschen, and Matthew Stave between 2019 and 2022. The files that the Yucatec Maya DoReCo dataset are based on are part of a larger collection of Stavros Skopeteas's Yucatec Maya data that is archived at TLA (https://hdl.handle.net/1839/00-0000-0000-0021-E91B-F). This dataset is made up by 10 audios files, with a length between 6 and 13 minutes, splitting the audios resulted in a total of 792 clips used in the training.

## Audio length

For both languages, audio length was kept between 3 and 15 seconds, audios longer than 15 seconds were divided into several clips, this division was done using the code found in "split_audios.py"  

# Spectrograms
A total of 3820 were generated and used in the training, 2215 from mexican spanish audios and 1705 from yucatec maya audios.
All spectrograms can be found in the "spanish_spectrograms" and "mayan_spectrograms" folders

# Model training

The file "Audio Classification (CNN).ipynb" found in the repository contains all the necessary code to perform the training once the audio data has been collected. The contents of the notebook include an adaptation and some additional functions based on the one found at https://github.com/jeffprosise/Deep-Learning/blob/master/Audio%20Classification%20(CNN).ipynb [5].

Although the "Audio Classification (CNN).ipynb" file describes the procedure for a single model, three separate training processes were carried out using a different base model for each. The currently used base model can be identified by examining the following code snippet:


```from tensorflow.keras.applications import MobileNetV2
from tensorflow.keras.applications.mobilenet import preprocess_input

base_model = MobileNetV2(weights='imagenet', include_top=False, input_shape=(224, 224, 3))
```


In the previous code snippet, MobileNetV2 is used as the base model. The other two base models used were ResNet50 and ResNet152.
To perform training with these base models, the previous code snippet should be replaced with one of the following, depending on the base model to use:

```from tensorflow.keras.applications import ResNet50
from tensorflow.keras.applications.resnet import preprocess_input

base_model = ResNet50(weights='imagenet', include_top=False, input_shape=(224, 224, 3))
```

```from tensorflow.keras.applications import ResNet152
from tensorflow.keras.applications.resnet import preprocess_input

base_model = ResNet152(weights='imagenet', include_top=False, input_shape=(224, 224, 3))
```

# Referencias
[1] Mukherjee, H., Ghosh, S., Sen, S., Sk Md, O., Santosh, K. C., Phadikar, S., & Roy, K. (2019). Deep learning for spoken language identification: Can we visualize speech signal patterns?. Neural Computing and Applications, 31, 8483-8501. 
[2] Ciempiess-unam. Recuperado de https://ciempiess.org/downloads 
[3] T’aantsil. Recuperado de https://taantsil.com.mx/ 
[4] Skopeteas, Stavros, Amedee Colli Colli, Daniela Schellenbach, Carolin Brokmann, Florian Fischer and Maya Gálvez Wimmelmann. 2024. Yucatec Maya DoReCo dataset. In Seifart, Frank, Ludger Paschen and Matthew Stave (eds.). Language Documentation Reference Corpus (DoReCo) 2.0. Lyon: Laboratoire Dynamique Du Langage (UMR5596, CNRS & Université Lyon 2). (https://doi.org/10.34847/nkl.9cbb3619). 
[5] Jeff Prosise (2021). Deep-Learning [Software]. GitHub. https://github.com/jeffprosise/Deep-Learning/blob/master/Audio%20Classification%20(CNN).ipynb 