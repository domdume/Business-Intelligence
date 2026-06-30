# <center> **ESCUELA POLITÉCNICA NACIONAL** </center>
# <center> **Business Intelligence** </center>
# <center> **Practica 10** </center>

**Integrantes**
* Doménica J. Cárdenas
* Danna Morales
* Salma Morales
* Belén Cholango
* Gabriel del Valle

Abrir el dataset leon_risk 
<img width="942" height="665" alt="image" src="https://github.com/user-attachments/assets/ee1f21fb-c26d-479f-906c-fc79b4b9b260" />

Ignorar atributos

<img width="1248" height="605" alt="image" src="https://github.com/user-attachments/assets/0b47e48e-50d0-4d4a-b555-233feae367db" />

Clustering primera corrida 
<img width="1261" height="895" alt="image" src="https://github.com/user-attachments/assets/96de3c57-dccd-4ec4-b487-50f7d3db0fdb" />

numClusters        Within cluster SSE
2                        (1519.0)
3                        (1106.0)
4                        (1010.0)
5(anota)
6(anota)

Mirando las caídas del error entre cada paso:

de k=2 a k=3: baja de 1519 a 1106 → mejora de 413
de k=3 a k=4: baja de 1106 a 1010 → mejora de 96

La mejora se reduce drásticamente después de k=3 (de 413 a 96, casi una cuarta parte). Eso es justamente el "codo": el punto donde añadir más clusters deja de aportar reducción significativa del error. Según estos datos, el número óptimo sería k=3.

**Tabla**
<img width="768" height="371" alt="image" src="https://github.com/user-attachments/assets/c77bbf28-12c9-4e78-b9ec-5dca11cb2c9f" /> 

**Grafico** 
<img width="942" height="371" alt="image" src="https://github.com/user-attachments/assets/84bc8444-9f64-43c4-b9ad-2cb19e26a9d8" />

Resultado con el numeor de clusters encontrado 
<img width="1261" height="895" alt="image" src="https://github.com/user-attachments/assets/f2318391-747e-4b74-a0d1-9fafa04c9ebf" />

**Análisis** 

El algoritmo SimpleKMeans agrupó las 1000 instancias en tres clusters. Cada cluster muestra un perfil de riesgo bien definido por sus centroides: el Cluster 0 reúne perfiles claramente riesgosos (edad media, ingreso bajo e historial crediticio pobre), el Cluster 2 agrupa perfiles seguros (adultos mayores, ingreso medio e historial bueno), mientras que el Cluster 1 (jóvenes, ingreso alto, historial promedio) resulta ambiguo y Weka no logra asignarle una clase dominante (No class). Al comparar contra la etiqueta real Loan_Decision, la matriz de confusión arroja un 42.3% de instancias mal agrupadas, un resultado pobre que se explica porque el método del codo sugirió 3 clusters frente a las solo 2 clases reales (risky/safe): ese cluster intermedio sin clase asignada divide y mezcla casos de ambas categorías, degradando la correspondencia. 
En conclusión, aunque el clustering revela estructura interna en los datos, su capacidad para reproducir la clasificación original de riesgo es limitada.



