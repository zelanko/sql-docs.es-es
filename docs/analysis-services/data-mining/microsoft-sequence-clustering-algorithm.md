---
title: Algoritmo de clústeres de secuencia de Microsoft | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 273d1271d63ae8f4d40d604745cbe8c3f5eda6ee
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="microsoft-sequence-clustering-algorithm"></a>Algoritmo de clústeres de secuencia de Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo único que combina el análisis secuencial con la agrupación en clústeres. Puede usar este algoritmo para explorar datos que contienen eventos que pueden vincularse con rutas o *secuencias*. El algoritmo encuentra las secuencias más comunes y realiza una agrupación en clústeres para buscar secuencias que sean similares. En los ejemplos siguientes se muestran los tipos de secuencia que se pueden capturar como datos para el aprendizaje automático con el fin de proporcionar información sobre problemas comunes o escenarios empresariales:  
  
-   Secuencias de clics o rutas de clics generadas cuando un usuario navega o examina un sitio web.  
  
-   Registros que enumeran eventos que preceden a un incidente, como errores de disco duro o interbloqueos del servidor.  
  
-   Registros de transacciones que describen el orden en el que un cliente agrega elementos a un carro de la compra en línea.  
  
-   Registros que siguen las interacciones del cliente (o paciente) a lo largo del tiempo para predecir cancelaciones del servicio u otros resultados poco satisfactorios.  
  
 Este algoritmo es similar en muchas maneras al algoritmo de clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Sin embargo, en lugar de encontrar clústeres de casos que contienen atributos similares, el algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] encuentra clústeres de casos que contienen rutas similares en una secuencia.  
  
## <a name="example"></a>Ejemplo  
 El sitio web de [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] recopila información sobre las páginas que visitan los usuarios y sobre el orden en que las visitan. Debido a que la empresa ofrece un sistema de pedidos en línea, los clientes deben registrarse en el sitio. Esto permite que la empresa pueda conseguir información de clics por cada perfil de cliente. Mediante el uso del algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] en estos datos, la empresa puede encontrar grupos, o clústeres, de los clientes que tienen patrones o secuencias de clics similares. La empresa puede usar estos clústeres para analizar la forma en que los clientes se mueven por el sitio web, identificar qué páginas se relacionan más estrechamente con la venta de un producto en particular y predecir las páginas que tienen mayores probabilidades de ser visitadas a continuación.  
  
## <a name="how-the-algorithm-works"></a>Cómo funciona el algoritmo  
 El algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es un algoritmo híbrido que combina técnicas de agrupación en clústeres con el análisis de cadenas de Markov para identificar los clústeres y sus secuencias.  Una de las marcas distintivas del algoritmo de clústeres de secuencia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] es que utiliza los datos de las secuencias. Estos datos suelen representar una serie de eventos o transiciones entre los estados de un conjunto de datos, como una serie de compras de productos o los clics en web para un usuario determinado. El algoritmo examina todas las probabilidades de transición y mide las diferencias, o las distancias, entre todas las posibles secuencias del conjunto de datos con el fin de determinar qué secuencias es mejor utilizar como entradas para la agrupación en clústeres. Cuando el algoritmo cree la lista de secuencias candidatas, usará la información de las secuencias como entrada para el método EM (maximización de la expectativa) de agrupación en clústeres.  
  
 Para obtener una descripción detallada de la implementación, vea [Microsoft Sequence Clustering Algorithm Technical Reference](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## <a name="data-required-for-sequence-clustering-models"></a>Datos requeridos para los modelos de clústeres de secuencias  
 Al preparar los datos para usarlos en el entrenamiento de un modelo de agrupación en clústeres de secuencia, conviene comprender qué requisitos son imprescindibles para el algoritmo concreto, incluidos el volumen de datos necesario y la forma en que se usan los datos.  
  
 Los requisitos de un modelo de agrupación en clústeres de secuencia son los siguientes:  
  
-   **Una columna de clave única** Un modelo de agrupación en clústeres de secuencia necesita una clave que identifique los registros.  
  
-   **Una columna de secuencia** : para los datos de la secuencia, el modelo debe tener una tabla anidada que contenga una columna de identificador de secuencia. El id. de secuencia puede ser cualquier tipo de datos ordenable. Por ejemplo, puede usar el identificador de una página web, un número entero o una cadena de texto, con tal de que la columna identifique los eventos en una secuencia. Solo se admite un identificador de secuencia por cada secuencia y un tipo de secuencia en cada modelo.  
  
-   **Atributos opcionales no relacionados con la secuencia** : el algoritmo admite la incorporación de otros atributos que no tengan que ver con las secuencias. Estos atributos pueden incluir las columnas anidadas.  
  
 Como muestra, en el ejemplo citado anteriormente del sitio web de [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , un modelo de agrupación en clústeres de secuencia podría incluir información de los pedidos como tabla de casos, datos demográficos sobre el cliente concreto de cada pedido como atributos no relacionados con la secuencia y una tabla anidada que contenga la secuencia que siguió el cliente al examinar el sitio o colocar los artículos en el carro de la compra como información de la secuencia.  
  
 Para obtener información más detallada sobre los tipos de contenido y los tipos de datos compatibles con los modelos de agrupación en clústeres, vea la sección Requisitos de [Referencia técnica del algoritmo de clústeres de secuencia de Microsoft](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md).  
  
## <a name="viewing-a-sequence-clustering-model"></a>Ver un modelo de agrupación en clústeres de secuencia  
 El modelo de minería de datos que crea este algoritmo contiene descripciones de las secuencias más comunes en los datos. Para explorar el modelo, puede usar el **Visor de clústeres de secuencia de Microsoft**. Cuando se ve un modelo de agrupación en clústeres de secuencia, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] muestra los clústeres que contienen varias transiciones. También pueden verse las estadísticas pertinentes. Para más información, vea [Examinar un modelo usando el Visor de clústeres de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md).  
  
 Si desea obtener más detalles, puede examinar el modelo en el [Visor de árbol de contenido genérico de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-generic-content-tree-viewer.md). El contenido almacenado para el modelo incluye la distribución para todos los valores de cada nodo, la probabilidad de cada clúster y detalles acerca de las transiciones. Para más información, vea [Contenido del modelo de minería de datos para los modelos de agrupación en clústeres &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md).  
  
## <a name="creating-predictions"></a>Crear predicciones  
 Una vez entrenado el modelo, los resultados se almacenan como un conjunto de patrones. Puede usar las descripciones de las secuencias más comunes en los datos para predecir el siguiente paso probable de una nueva secuencia. Sin embargo, dado que el algoritmo incluye otras columnas, puede usar el modelo resultante para identificar las relaciones entre los datos de las secuencias y las entradas que no son secuenciales. Por ejemplo, si agrega datos demográficos al modelo, puede realizar predicciones para grupos concretos de clientes. Las consultas de predicción se pueden personalizar para que devuelvan un número variable de predicciones o estadísticas descriptivas.  
  
 Para obtener información sobre cómo crear consultas en un modelo de minería de datos, vea [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md). Para consultar ejemplos de cómo usar las consultas con un modelo de agrupación en clústeres, vea [Ejemplos de consultas de modelos de clústeres de secuencia](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md).  
  
## <a name="remarks"></a>Comentarios  
  
-   No se admite el uso del Lenguaje de marcado de modelos de predicción (PMML) para crear modelos de minería de datos.  
  
-   Admite la obtención de detalles.  
  
-   Admite el uso de modelos de minería de datos OLAP y la creación de dimensiones de minería de datos.  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos & #40; Analysis Services: minería de datos & #41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Referencia técnica del algoritmo de agrupación en clústeres de secuencia de Microsoft](../../analysis-services/data-mining/microsoft-sequence-clustering-algorithm-technical-reference.md)   
 [Ejemplos de consultas de modelo de clústeres de secuencia](../../analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [Examinar un modelo usando el Visor de clústeres de secuencia de Microsoft](../../analysis-services/data-mining/browse-a-model-using-the-microsoft-sequence-cluster-viewer.md)  
  
  
