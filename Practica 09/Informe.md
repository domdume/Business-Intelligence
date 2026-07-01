# <center> **ESCUELA POLITÉCNICA NACIONAL** </center>
# <center> **Business Intelligence** </center>
# <center> **Practica 9** </center>
# <center> **GRSW2** </center>

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
**Figura 1.** Carga del conjunto de datos weather.nominal.arff en Weka.

- En la pestaña Classify seleccionar el clasificador NaiveBayes.
- En "More Options" dejar valores por defecto.
- Seleccionar la opción "Use Training Set" en la ventana de set options.
- Ejecutar el entrenamiento del modelo.
<img width="845" height="772" alt="image" src="https://github.com/user-attachments/assets/95b81757-2198-495c-a4c6-96b69f0a940f" />
**Figura 2.** Configuración de dataset.

### Resultados

Al ejecutar el clasificador, Weka muestra la información del modelo generado y las probabilidades calculadas para cada atributo del conjunto de datos.

<img width="1263" height="477" alt="image" src="https://github.com/user-attachments/assets/f5019d9a-7cde-4b43-ae36-0488f702dd18" />
**Figura 3.** Primera sección de resultados: Información de la ejecución y clasificación del modelo.

También se presentan las probabilidades asociadas a cada atributo y clase, las cuales son utilizadas por el algoritmo para realizar la clasificación.

<img width="1258" height="752" alt="image" src="https://github.com/user-attachments/assets/b9fd3bfe-5a45-45e0-ad4d-d50d46db27c7" />
**Figura 4.** Segunda sección de resultados: Clases.

Weka muestra el resumen de la evaluación del modelo. Se obtuvo una precisión del **92.8571 %**, con **13 instancias clasificadas correctamente** y **1 instancia clasificada incorrectamente**. Además, se presenta la matriz de confusión, que resume el desempeño del clasificador.

<img width="1253" height="773" alt="image" src="https://github.com/user-attachments/assets/fb0ecb3e-0799-4a62-8a9b-9af09728816c" />
**Figura 5.** Tercera sección de resultados: Summary, matriz de confusión y precisión obtenida.

Lo siguiente fue implementar el algoritmo en **Google Colab** utilizando el código proporcionado durante la práctica.

<img width="1157" height="701" alt="image" src="https://github.com/user-attachments/assets/7250d7e8-ba48-40fd-b0c7-b6d1eb775961" />
**Figura 6.** Código en google collab: parte 1.

<img width="1163" height="643" alt="image" src="https://github.com/user-attachments/assets/a8b43467-fb5d-4215-bd43-5fc897832ee1" />
**Figura 7.** Código en google collab: parte 2.

Tras ejecutar el programa e ingresar los valores solicitados, se obtuvo la predicción correspondiente según las probabilidades calculadas por el modelo.

<img width="460" height="251" alt="image" src="https://github.com/user-attachments/assets/95fb58b0-8b79-49a0-9e96-3f9419a6d403" />
**Figura 8.** Resultado de predicción calculado por el modelo para valores sunny/hot/high/false: NO JUGAR.

## Predecir valores

...

# Referencias bibliográficas

...

# Declaración de uso de IA

Para la elaboración de este informe se utilizó inteligencia artificial (ChatGPT) como herramienta de apoyo para la redacción del documento, organización del contenido y revisión de la estructura. Su uso corresponde aproximadamente al 20% del trabajo total. El análisis, desarrollo de la práctica, ejecución en Weka y validación de resultados fueron realizados por los integrantes del grupo.
