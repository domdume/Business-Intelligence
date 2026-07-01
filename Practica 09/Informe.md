# <center> **ESCUELA POLITÉCNICA NACIONAL** </center>
# <center> **Business Intelligence** </center>
# <center> **Practica 9** </center>
# <center> **GR2SW** </center>

**Integrantes**
* Doménica J. Cárdenas
* Danna Morales
* Salma Morales
* Belén Cholango
* Gabriel del Valle

**Fecha:** 30/06/2026

## **Índice de Contenidos**

1. [Introducción](#introducción)
2. [Desarrollo](#desarrollo)
   - [Naive Bayes](#naive-bayes)
   - [Predecir valores](#predecir-valores)
3. [Referencias bibliográficas](#referencias-bibliográficas)
4. [Declaración de uso de IA](#declaración-de-uso-de-ia)

# Introducción

En esta práctica se utilizó Weka para aplicar el algoritmo de clasificación Naive Bayes sobre el conjunto de datos `weather.nominal.arff`. Luego, se implementó el modelo en Python y se realizaron predicciones de nuevas instancias utilizando Weka. El objetivo fue comprender el funcionamiento del algoritmo y analizar los resultados obtenidos.

# Desarrollo

## Naive Bayes

Se realizaron los siguientes pasos para entrenar el modelo Naive Bayes en Weka:
- Abrir Weka Explorer.
- Cargar el dataset weather.nominal.arf.

<img width="933" height="662" alt="image" src="https://github.com/user-attachments/assets/d4ec32c2-fbaa-4c6d-9a32-21371e7af956" />
<p align="center"><i>Figura 1: Carga del conjunto de datos weather.nominal.arff en Weka.</i></p>

- En la pestaña Classify seleccionar el clasificador NaiveBayes.
- En "More Options" dejar valores por defecto.
- Seleccionar la opción "Use Training Set" en la ventana de set options.
- Ejecutar el entrenamiento del modelo.
<img width="845" height="772" alt="image" src="https://github.com/user-attachments/assets/95b81757-2198-495c-a4c6-96b69f0a940f" />
<p align="center"><i>Figura 2: Configuración de dataset.</i></p>

### Resultados

Al ejecutar el clasificador, Weka muestra la información del modelo generado y las probabilidades calculadas para cada atributo del conjunto de datos.

<img width="1263" height="477" alt="image" src="https://github.com/user-attachments/assets/f5019d9a-7cde-4b43-ae36-0488f702dd18" />
<p align="center"><i>Figura 3: Primera sección de resultados: Información de la ejecución y clasificación del modelo.</i></p>

También se presentan las probabilidades asociadas a cada atributo y clase, las cuales son utilizadas por el algoritmo para realizar la clasificación.

<img width="1258" height="752" alt="image" src="https://github.com/user-attachments/assets/b9fd3bfe-5a45-45e0-ad4d-d50d46db27c7" />
<p align="center"><i>Figura 4: Segunda sección de resultados: Clases.</i></p>

Weka muestra el resumen de la evaluación del modelo. Se obtuvo una precisión del **92.8571 %**, con **13 instancias clasificadas correctamente** y **1 instancia clasificada incorrectamente**. Además, se presenta la matriz de confusión, que resume el desempeño del clasificador.

<img width="1253" height="773" alt="image" src="https://github.com/user-attachments/assets/fb0ecb3e-0799-4a62-8a9b-9af09728816c" />
<p align="center"><i>Figura 5: Tercera sección de resultados: Summary, matriz de confusión y precisión obtenida.</i></p>

Lo siguiente fue implementar el algoritmo en **Google Colab** utilizando el código proporcionado durante la práctica.

<img width="1157" height="701" alt="image" src="https://github.com/user-attachments/assets/7250d7e8-ba48-40fd-b0c7-b6d1eb775961" />
<p align="center"><i>Figura 6: Código en google collab: parte 1.</i></p>

<img width="1163" height="643" alt="image" src="https://github.com/user-attachments/assets/a8b43467-fb5d-4215-bd43-5fc897832ee1" />
<p align="center"><i>Figura 7: Código en google collab: parte 2.</i></p>

Tras ejecutar el programa e ingresar los valores solicitados, se obtuvo la predicción correspondiente según las probabilidades calculadas por el modelo.

<img width="460" height="251" alt="image" src="https://github.com/user-attachments/assets/95fb58b0-8b79-49a0-9e96-3f9419a6d403" />
<p align="center"><i>Figura 8: Resultado de predicción calculado por el modelo para valores sunny/hot/high/false: NO JUGAR.</i></p>

## Predecir valores

Para realizar la predicción de nuevas instancias utilizando el clasificador Naive Bayes en Weka, se siguieron los siguientes pasos:

- Abrir **Tools** desde el menú principal de Weka.
- Seleccionar **ArffViewer**.
- Ir a **File → Open** y cargar el conjunto de datos `weather.nominal.arff`.

<img width="1107" height="835" alt="image" src="https://github.com/user-attachments/assets/4f0a186a-1185-42f9-865e-fc1eacd6d442" />
<p align="center"><i>Figura 9: Carga del conjunto de datos weather.nominal.arff en Weka para predecir valores.</i></p>

Se seleccionaron todas las instancias del conjunto de datos excepto una y se eliminaron, dejando únicamente un registro para utilizarlo como caso de prueba.

<img width="475" height="510" alt="image" src="https://github.com/user-attachments/assets/b01a817d-6a0e-4f50-815e-386aa0e50cb7" />
<p align="center"><i>Figura 10: Elimincación de 13 registros</i></p>

Se modificaron los valores del registro restante y se dejó en blanco el atributo de clase (**play**), ya que este sería predicho por el clasificador.

<img width="482" height="182" alt="image" src="https://github.com/user-attachments/assets/21eb31be-f32b-4899-9257-670e30e2ec4b" />
<p align="center"><i>Figura 11: Modificación de valores en el único registro.</i></p>

Una vez editado el registro, el archivo se guardó con el nombre **test.arff**.

Después, en **Weka Explorer**, se realizaron los siguientes pasos:

- Cargar nuevamente el archivo `weather.nominal.arff`.
- Abrir la pestaña **Classify**.
- Seleccionar el clasificador **NaiveBayes**.
- Cambiar el método de evaluación de **Use Training Set** a **Supplied Test Set**.
- Hacer clic en **Set** y cargar el archivo `test.arff`.
- En **More Options**, seleccionar **PlainText** en la opción **Output predictions**.

<img width="835" height="750" alt="image" src="https://github.com/user-attachments/assets/1adfb5d9-10e9-4adb-99a9-f6cd9aab7d5b" />
<p align="center"><i>Figura 12: Selección de PlainTest en la ventana emergente "More Options".</i></p>

Se ejecutó el clasificador. El resultado obtenido indicó que la instancia de prueba fue clasificada con el valor **"yes"**, correspondiente a la clase predicha por Naive Bayes.

<img width="1012" height="291" alt="image" src="https://github.com/user-attachments/assets/0477ed9f-fe3c-41a9-abf6-4e5c71580ad8" />
<p align="center"><i>Figura 13: Resultado de predicción con NaiveBayes.</i></p>

Como comparación, se repitió el procedimiento utilizando el clasificador **J48**, obteniéndose igualmente la predicción para la instancia de prueba.

<img width="841" height="445" alt="image" src="https://github.com/user-attachments/assets/701f5683-7fef-450e-8d45-a12ba2f842f4" />
<p align="center"><i>Figura 14: Resultado de predicción con J48.</i></p>

En este caso, tanto Naive Bayes como J48 predijeron la misma clase (yes), lo que indica que ambos clasificadores coincidieron para la instancia de prueba utilizada.

# Referencias bibliográficas

[1] D. Martínez, “CLASIFICACIÓN,” guía de práctica de laboratorio, Escuela Politécnica Nacional, Quito, Ecuador, 2026.

# Declaración de uso de IA

Para la elaboración de este informe se utilizó inteligencia artificial (ChatGPT) como herramienta de apoyo para la redacción del documento, organización del contenido y revisión de la estructura. Su uso corresponde aproximadamente al 15% del trabajo total. El análisis, desarrollo de la práctica, ejecución en Weka y validación de resultados fueron realizados por los integrantes del grupo.
