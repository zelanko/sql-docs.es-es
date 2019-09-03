---
title: 'Tutorial: Creación de un modelo de agrupación en clústeres en Python'
description: En la tercera parte de esta serie de tutoriales de cuatro partes, creará un modelo de K-means para realizar la agrupación en clústeres en Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ce7f6cbd580afbdbf71065803af8d394323e5dc3
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211979"
---
# <a name="tutorial-build-a-clustering-model-in-python-with-sql-server-machine-learning-services"></a>Tutorial: Cree un modelo de agrupación en clústeres en Python con SQL Server Machine Learning Services

En la tercera parte de esta serie de tutoriales de cuatro partes, creará un modelo de K-means en Python para realizar la agrupación en clústeres. En la siguiente parte de esta serie, implementará este modelo en una base de datos SQL con SQL Server Machine Learning Services.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Definir el número de clústeres para un algoritmo K-means
> * Realizar agrupación en clústeres
> * Analizar los resultados

En la [primera parte](tutorial-python-clustering-model.md), instaló los requisitos previos e importó la base de datos de ejemplo.

En la [segunda parte](tutorial-python-clustering-model-prepare-data.md), aprendió a preparar los datos de una base de datos SQL para realizar la agrupación en clústeres.

En la [cuarta parte](tutorial-python-clustering-model-deploy.md), aprenderá a crear un procedimiento almacenado en una base de datos SQL que puede realizar la agrupación en clústeres en Python en función de los nuevos datos.

## <a name="prerequisites"></a>Requisitos previos

* En la tercera parte de este tutorial se da por supuesto que se han cumplido los requisitos previos de la [**parte uno**](tutorial-python-clustering-model.md)y se han completado los pasos de la [**segunda parte**](tutorial-python-clustering-model-prepare-data.md).

## <a name="define-the-number-of-clusters"></a>Definir el número de clústeres

Para agrupar los datos del cliente, usará el algoritmo de agrupación en clústeres **K-means** , una de las formas más sencillas y conocidas de agrupar los datos.
Puede obtener más información acerca de K-means en [una guía completa del algoritmo de agrupación en clústeres k-means](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html).

El algoritmo acepta dos entradas: Los propios datos y un número predefinido "*k*" que representa el número de clústeres que se van a generar.
La salida es de *k* clústeres con los datos de entrada particionados entre los clústeres.

El objetivo de K-means es agrupar los elementos en clústeres k de modo que todos los elementos del mismo clúster sean similares entre sí y, como sea posible, de los elementos de otros clústeres.

Para determinar el número de clústeres que va a usar el algoritmo, use un trazado de dentro de grupos suma de cuadrados, mediante el número de clústeres extraídos. El número de clústeres adecuado que se va a usar es el plegado o el "codo" del trazado.

```python
################################################################################################
## Determine number of clusters using the Elbow method
################################################################################################

cdata = customer_data
K = range(1, 20)
KM = (sk_cluster.KMeans(n_clusters=k).fit(cdata) for k in K)
centroids = (k.cluster_centers_ for k in KM)

D_k = (sci_distance.cdist(cdata, cent, 'euclidean') for cent in centroids)
dist = (np.min(D, axis=1) for D in D_k)
avgWithinSS = [sum(d) / cdata.shape[0] for d in dist]
plt.plot(K, avgWithinSS, 'b*-')
plt.grid(True)
plt.xlabel('Number of clusters')
plt.ylabel('Average within-cluster sum of squares')
plt.title('Elbow for KMeans clustering')
plt.show()
```

![Gráfico de codo](./media/python-tutorial-elbow-graph.png)

En función del gráfico, se parece a *k = 4* , que sería un buen valor. Ese valor *k* agrupará a los clientes en cuatro clústeres.

## <a name="perform-clustering"></a>Realizar agrupación en clústeres

En el siguiente script de Python, usará la función KMeans del paquete sklearn.

```python
################################################################################################
## Perform clustering using Kmeans
################################################################################################

# It looks like k=4 is a good number to use based on the elbow graph.
n_clusters = 4

means_cluster = sk_cluster.KMeans(n_clusters=n_clusters, random_state=111)
columns = ["orderRatio", "itemsRatio", "monetaryRatio", "frequency"]
est = means_cluster.fit(customer_data[columns])
clusters = est.labels_
customer_data['cluster'] = clusters

# Print some data about the clusters:

# For each cluster, count the members.
for c in range(n_clusters):
    cluster_members=customer_data[customer_data['cluster'] == c][:]
    print('Cluster{}(n={}):'.format(c, len(cluster_members)))
    print('-'* 17)
print(customer_data.groupby(['cluster']).mean())
```

## <a name="analyze-the-results"></a>Analizar los resultados

Ahora que ha realizado la agrupación en clústeres con K-means, el siguiente paso es analizar el resultado y ver si puede encontrar información procesable.

Observe los valores medios de la agrupación en clústeres y los tamaños de clúster impresos desde el script anterior.

```results
Cluster0(n=31675):
-------------------
Cluster1(n=4989):
-------------------
Cluster2(n=1):
-------------------
Cluster3(n=671):
-------------------

         customer  orderRatio  itemsRatio  monetaryRatio  frequency
cluster
0        50854.809882    0.000000    0.000000       0.000000   0.000000
1        51332.535779    0.721604    0.453365       0.307721   1.097815
2        57044.000000    1.000000    2.000000     108.719154   1.000000
3        48516.023845    0.136277    0.078346       0.044497   4.271237
```

Los cuatro medios del clúster se proporcionan mediante las variables definidas en la [parte uno](tutorial-python-clustering-model-prepare-data.md#separate-customers):

* *orderRatio* = proporción del orden de retorno (número total de pedidos parcialmente o totalmente devueltos frente al número total de pedidos)
* *itemsRatio* = relación de los elementos devueltos (número total de elementos devueltos frente al número de elementos comprados)
* *monetaryRatio* = proporción del importe de retorno (importe monetario total de los artículos devueltos frente al importe adquirido)
* *Frequency* = frecuencia de devolución

La minería de datos mediante K-means a menudo requiere un análisis más profundo de los resultados y pasos adicionales para comprender mejor cada clúster, pero puede proporcionar buenos clientes potenciales.
Estas son algunas formas de interpretar estos resultados:

* Cluster 0 parece ser un grupo de clientes que no están activos (todos los valores son cero).
* Cluster 3 parece ser un grupo que destaca en términos de comportamiento de retorno.

Cluster 0 es un conjunto de clientes claramente inactivos. Quizás puede dirigirse a los esfuerzos de marketing hacia este grupo para desencadenar un interés en las compras. En el paso siguiente, realizará una consulta en la base de datos de las direcciones de correo electrónico de los clientes del clúster 0, para que pueda enviarle un correo electrónico de marketing.

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va a continuar con este tutorial, elimine la base de datos tpcxbb_1gb de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

En la tercera parte de esta serie de tutoriales, ha completado estos pasos:

* Definir el número de clústeres para un algoritmo K-means
* Realizar agrupación en clústeres
* Analizar los resultados

Para implementar el modelo de aprendizaje automático que ha creado, siga la cuarta parte de esta serie de tutoriales:

> [!div class="nextstepaction"]
> [Tutorial: Implementación de un modelo de agrupación en clústeres en Python con SQL Server Machine Learning Services](tutorial-python-clustering-model-deploy.md)