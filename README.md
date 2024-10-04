# PROCESAMIENTO DE SEÑAL EMG
## Adquisición de la señal EMG
La señal se adquirió principalmente de tres músculos: el flexor ulnar del carpo, el flexor radial del carpo y el flexor profundo de los dedos. A continuación, se detallará la ubicación de los electrodos como la señal adquirida originalmente sin filtros:
<img src="https://github.com/user-attachments/assets/a4c3d7df-bed1-4b32-b198-4145f54d3630" width="700" alt="Imagen 2" style="display: inline-block;"/>
<img src="https://github.com/user-attachments/assets/cf881c67-99cb-4407-b10a-79112734a435" width="200" alt="Imagen 1" style="display: inline-block;"/>

La señal original capturada presenta las siguientes características:
- **Frecuencia de muestreo**: 3000 Hz
- **Tiempo de muestreo**: 333.33 µs. Este valor se calculó a partir de la siguiente fórmula:
![WhatsApp Image 2024-10-03 at 5 36 18 PM](https://github.com/user-attachments/assets/839c2816-ae0b-4b3d-a4d2-33753edf9cb2)
- **Duración total de la señal**: 60 segundos, podemos comprobarlo a partir de:
![image](https://github.com/user-attachments/assets/0fa3b120-6e8b-4901-9fb5-7b0e1743fecb)

- **Número de contracciones**: 600 contracciones por minuto.

## Aplicación de las ventanas de Hanning 
Elegimos la ventana de Hanning para analizar la señal de electromiografía porque ofrece varias ventajas. Primero, suaviza la señal, lo que reduce las discontinuidades y distorsiones en el análisis de frecuencias, permitiendo una representación más precisa de las componentes de la señal.

Además, la ventana de Hanning mejora la resolución de frecuencias, lo cual es crucial para identificar patrones de activación muscular. Su transición gradual, en comparación con otras ventanas más abruptas, minimiza la alteración de la forma de onda original.

Por último, es especialmente útil para señales con componentes de frecuencia específicas, ya que ayuda a destacar esas frecuencias en el espectro.

En este caso decidimos analizar la ventana 591 porque es una de las ultimas contracciones hechas en el lapso de tiempo en que adquirimos los datos, pues a este punto el musculo estba llegando a la fatiga, hicimos 600 contracciones y por cada una de ellas una vantana de hanning, pero de estas ploteamos las ultimas 10 para visualizar la llegada a la fatiga muscular.

![image](https://github.com/user-attachments/assets/c8358c26-34e7-4200-8543-3b2ca19b6f45)

La ventana de Hanning, tiene un propósito específico en el análisis de una contracción muscular:
### 1. Forma de la Ventana:
La ventana de Hanning es una función de suavizado que, en términos visuales, parece una curva suave con los extremos que tienden a cero. Esto reduce el efecto de discontinuidades que podrían estar presentes si la señal se corta abruptamente. Además, hay una oscilación con un crecimiento progresivo hacia un pico central alrededor del tiempo 59.05 s, con amplitudes máximas y mínimas pronunciadas, que luego disminuyen suavemente hacia los lados. Esto es una señal de que la contracción muscular tiene un evento fuerte en ese momento central.
### 2. Tamaño de la Ventana:
En términos de tiempo, cada muestra en la ventana representa un pequeño intervalo de tiempo dentro de esa contracción. Se realizo la toma de 600 contracciones por minuto y por cada contracción se realizo una ventana, la que estamos analizando en la 591 ya que en este punto de está acercando a la fatiga muscular. En cuanto a la amplitud tiene un pico maximo hasta 400 mV y en este punto logramos ver la contración del musculo, el punto en donde esta por llegar a la fatiga.
### 3. Interpretación de la Contracción:
La forma ondulante en la gráfica indica la actividad muscular durante una contracción. Los picos positivos y negativos en la amplitud sugieren que la señal EMG está captando el esfuerzo del músculo al contraerse y relajarse.
El pico central más alto y con mayor amplitud alrededor de los 59.05 s indica el momento máximo de contracción muscular. El hecho de que los picos decrezcan gradualmente sugiere que el músculo se está relajando después de esta contracción máxima.
Esta ventana en particular se está utilizando para enfocar un segmento de la señal de EMG, en el momento más relevante de la contracción muscular.
El objetivo principal de aplicar una ventana de Hanning es evitar el efecto de discontinuidades en los bordes del segmento de señal, para que cuando se analice los resultados sean más precisos y con menos artefactos.
La señal muestra claramente una contracción muscular significativa dentro de este intervalo, destacando el pico máximo de esfuerzo.

A continuacion veremos  la señal antes como después de la convolución: 

![image](https://github.com/user-attachments/assets/18abcec3-fed3-4745-91c2-1a1eb7bfc094)

*Señal Original vs. Señal convolucionada*

   **- Señal Original (Azul):**
Esta es la señal inicial con picos de amplitud que llegan a valores cercanos a 400. La señal muestra un patrón oscilante más marcado y con amplitudes altas, lo que sugiere que el músculo tiene una actividad intensa y sin filtrar. Se pueden ver varias oscilaciones fuertes, especialmente en la región de tiempo entre 59.02 s y 59.08 s, lo que refleja la actividad eléctrica captada durante la contracción muscular.

   **- Señal convolucionada (Naranja):**
Al aplicar la ventana de Hanning de tamaño 591, la amplitud de la señal se ha suavizado considerablemente, y ahora los picos están en un rango mucho más bajo (máximos cercanos a 100). La ventana suaviza los bordes de la señal, atenuando las oscilaciones de alta frecuencia y reduciendo el impacto de variaciones bruscas que pueden aparecer en la señal original. Esto es útil para evitar interferencia en el análisis frecuencial posterior. Las oscilaciones en esta señal aún siguen el mismo patrón general que la señal original, pero están más moderadas y redondeadas y así no confundirlo con el ruido de alta frecuencia.

*Comparación entre Señales:*

**- Forma:**
     - La señal original es más ruidosa, con mayores oscilaciones y picos bruscos. Esto puede deberse a la presencia de componentes de alta frecuencia o artefactos del entorno.
     - La señal con la ventana de Hanning es mucho más suave, preservando la estructura básica, pero eliminando las fluctuaciones rápidas que podrían interferir en un análisis preciso.
   
 **-Tamaño:**
     - La señal original tiene amplitudes mucho más grandes, con picos que alcanzan valores cercanos a 400.
     - La señal con la ventana de Hanning está considerablemente reducida en amplitud, con valores máximos alrededor de 100, lo cual indica que la ventana ha atenuado las oscilaciones más fuertes y centrado la señal en sus componentes más relevantes.



