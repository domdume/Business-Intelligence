# <center> **ESCUELA POLITÉCNICA NACIONAL** </center>
# <center> **Business Intelligence** </center>
# <center> **Practica 10** </center>

**Integrantes**
* Doménica J. Cárdenas
* Danna Morales
* Salma Morales
* Belén Cholango
* Gabriel Del Valle

### Introducción
En esta práctica se aplicaron distintas técnicas en WEKA sobre el dataset de análisis crediticio. El objetivo fue agrupar los registros según sus características, sin considerar la etiqueta de clase, para identificar patrones presentes en los datos.

### Desarrollo
1. Abrir y cargar el dataset de análisis crediticio en WEKA.
<img width="932" height="658" alt="image" src="https://github.com/user-attachments/assets/2fc8c0ee-a4aa-493d-8c89-ec24c4c4859f" />

2. Se aplicó el algoritmo de clustering SimpleKMeans.
<img width="1260" height="946" alt="image" src="https://github.com/user-attachments/assets/27a1634a-8bd5-458b-a36c-f851d8f89507" />

3. Se modifico el parámetro numClusters con diferentes valores de K. Posteriormente se comparó el error cuadrático obtenido en cada ejecución para identificar el número óptimo de clusters. Finalmente, se realizó el clustering utilizando el valor de K seleccionado.
<img width="569" height="957" alt="image" src="https://github.com/user-attachments/assets/3a3cf73d-b9e1-4227-b1d3-916161dcf2bb" />

4. Se eliminó la etiqueta de clase del dataset utilizando la opción Ignore Attributes de WEKA, seleccionando únicamente el atributo correspondiente a la clase para que el algoritmo realizara el clustering únicamente con las variables descriptivas. 
<img width="1261" height="943" alt="image" src="https://github.com/user-attachments/assets/6f03dd3c-1dde-448a-b731-5d14b65a75cf" />

#### Resultados 
<img width="1258" height="951" alt="image" src="https://github.com/user-attachments/assets/43d08997-e8fa-4097-9323-3b1b66f75f29" />
Se ejecutó el algoritmo SimpleKMeans con K = 3, obteniendo tres grupos de 61, 50 y 39 instancias, que representan el 41 %, 33 % y 26 % del conjunto de datos, respectivamente. Los centroides muestran diferencias en las características de cada grupo, evidenciando una separación adecuada de los datos.
<br>

##### Clasess to cluster evaluation: 
Los tres clusters obtenidos representan adecuadamente las clases del dataset. El algoritmo presentó un 11,33 % de instancias mal agrupadas, logrando una clasificación mayormente correcta.
<img width="1261" height="947" alt="image" src="https://github.com/user-attachments/assets/9c341c1c-9518-4777-bd9e-8ca07ae2a369" />

##### Cluster matrix: 
<img width="1260" height="944" alt="image" src="https://github.com/user-attachments/assets/f025a70c-844d-4307-9e16-5bfdbf8ff1c2" />

##### Identificaci[on de centroides para cada cluster 
<img width="645" height="396" alt="image" src="https://github.com/user-attachments/assets/ddf80dbb-8ff7-4354-a0b3-33c4a7d31685" />

##### Añadir otro cluster al dataset 
<img width="1256" height="946" alt="image" src="https://github.com/user-attachments/assets/63b069c2-b458-416e-9cda-dca01078bc62" />

##### Configuración del addClustering 
<img width="1546" height="951" alt="image" src="https://github.com/user-attachments/assets/8768ef96-9a88-4c11-8ce1-e8e6b2eff32c" />

##### Resultados de aplicar las configuraciones del addclustering y el No class 
<img width="1265" height="948" alt="image" src="https://github.com/user-attachments/assets/cb4d4a89-49fe-4453-8910-c01396c87a76" />

##### Comparacion de valores del nuevo atributo del cluster añadido 
<img width="1231" height="741" alt="image" src="https://github.com/user-attachments/assets/799d138c-d774-4d1c-b611-47ca8ffb3602" />

Ver el arbol 
- Reglas de predicción:
  Se construyó un árbol de decisión J48 con 6 hojas y 11 nodos. El modelo obtuvo una precisión del 94,12 %, clasificando correctamente 48 de 51 instancias evaluadas.
  <img width="1261" height="945" alt="image" src="https://github.com/user-attachments/assets/2aeefeb6-6faa-40b6-9957-25821b05cf47" />
- Ver el arbol:
<img width="1263" height="949" alt="image" src="https://github.com/user-attachments/assets/36673159-111b-4287-820d-0c1313c57ef1" />

Commparación entre las reglas de predicción generado por el cluster y las no generadas por el cluster. 

##### Cluster: 
<img width="518" height="356" alt="image" src="https://github.com/user-attachments/assets/4fc1b9e4-a7ac-447d-80ee-55249d68e503" />

##### No cluster: 
<img width="441" height="261" alt="image" src="https://github.com/user-attachments/assets/fcc53493-c520-4620-840b-e0ad6f0201da" />

##### Simplificación del arbol 
<img width="438" height="253" alt="image" src="https://github.com/user-attachments/assets/61348ecf-fbf7-4585-9855-ef2debb977f1" />





















