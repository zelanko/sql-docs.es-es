---
title: Obtención de detalles en modelos de minería de datos | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2abd3430c1882148cd564c973ecf5824f3a55d4a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34014812"
---
# <a name="drillthrough-on-mining-models"></a>Obtención de detalles en modelos de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La*obtención de detalles* se refiere a la capacidad de consultar un modelo o una estructura de minería de datos y obtener datos detallados que no se exponen en el modelo.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]proporciona dos opciones diferentes para obtener detalles sobre los datos de los casos. Puede obtener detalles tanto de los casos usados para generar los datos como de los casos de la estructura de minería de datos.  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>Obtención de detalles de los casos del modelo frente a obtención de detalles de la estructura  
 La obtención de detalles de los **casos del modelo** resulta útil para buscar detalles adicionales sobre las reglas, los patrones o los clústeres de un modelo. Por ejemplo, no usaría información de contacto de cliente para el análisis en un modelo de clústeres, incluso si los datos estuvieran disponibles, mediante la obtención de detalles podría obtener acceso a la información del modelo.  
  
 En cambio, la **obtención de detalles de los datos de la estructura** pretende proporcionar acceso a la información que no está disponible en el modelo. Por ejemplo, algunas columnas de la estructura se han excluido de un modelo porque el tipo de datos era compatible o los datos no eran útiles para el análisis.  
  
## <a name="enabling-drillthrough-on-a-model"></a>Habilitar la obtención de detalles en un modelo  
 Para utilizar la obtención de detalles en un modelo de minería de datos, se deben cumplir las condiciones siguientes:  
  
-   Es posible configurar la obtención de detalles solo en los casos de modelos y no en la estructura de minería de datos, pero no al contrario.  Es decir, la obtención de detalles debe estar habilitada en el modelo de minería de datos para permitir la obtención de detalles en la estructura de minería de datos.  
  
-   La obtención de detalles en el modelo y la estructura está deshabilitada de forma predeterminada. Si usa el Asistente para minería de datos, la opción para habilitar la obtención de detalles en los casos del modelo está en la página final del asistente.  
  
-   Puede agregar la capacidad de obtener detalles a un modelo de minería de datos existente pero, si lo hace, hay que volver a procesar el modelo para poder obtener detalles de los datos.  
  
-   La obtención de detalles no funcionará a menos que se haya mantenido la memoria caché creada durante el proceso de entrenamiento. Para más información sobre las propiedades que controlan el almacenamiento en caché, vea [Obtención de detalles en estructuras de minería de datos](../../analysis-services/data-mining/drillthrough-on-mining-structures.md).  
  
## <a name="models-that-support-drillthrough"></a>Modelos compatibles con la obtención de detalles  
 Si se ha configurado un modelo de minería de datos para permitir la obtención de detalles y tiene los permisos adecuados, al examinar el modelo puede hacer clic en un nodo en el visor adecuado y recuperar la información detallada sobre los casos de ese nodo concreto.  
  
 No todos los modelos son compatibles con la obtención de detalles; depende del algoritmo utilizado para crear el modelo. En la tabla siguiente se enumeran los tipos de modelos que no son compatibles con la obtención de detalles o que lo son con limitaciones. Si el tipo de modelo no aparece, es compatible con la obtención de detalles.  
  
|**Nombre del algoritmo**|**Es compatible con la obtención de detalles**|  
|------------------------|----------------------------------|  
|Algoritmo Bayes Naïve de Microsoft|No compatible.<br /><br /> Estos algoritmos no asignan casos a nodos específicos del contenido.|  
|Algoritmo de red neuronal de Microsoft|No compatible.<br /><br /> Estos algoritmos no asignan casos a nodos específicos del contenido.|  
|Algoritmo de regresión logística de Microsoft|No compatible.<br /><br /> Estos algoritmos no asignan casos a nodos específicos del contenido.|  
|Algoritmo de regresión lineal de Microsoft|Compatible.<br /><br /> Sin embargo, dado que el modelo crea un único nodo, **All**, la obtención de detalles devuelve todos los casos de entrenamiento para el modelo. Si el conjunto de entrenamiento es grande, la carga de resultados puede tardar mucho tiempo.|  
|Algoritmo de serie temporal de Microsoft|Compatible.<br /><br /> Sin embargo, no puede obtener información de estructuras o casos mediante el **Visor de modelos de minería de datos** en el Diseñador de minería de datos. En su lugar, debe crear una consulta de DMX.<br /><br /> Tampoco puede obtener detalles de nodos específicos, ni escribir una consulta DMX para recuperar casos en nodos específicos de un modelo de serie temporal. Puede recuperar datos de casos del modelo o la estructura usando otros criterios, como valores de fecha o de atributo.<br /><br /> Si quiere ver detalles de los nodos ARTXP y ARIMA creados por el algoritmo de serie temporal de Microsoft, podría ser más fácil usar [Visor de árbol de contenido genérico de Microsoft &#40;Minería de datos&#41;](http://msdn.microsoft.com/library/751b4393-f6fd-48c1-bcef-bdca589ce34c).|  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 Vea los temas siguientes para obtener más información sobre el uso de la obtención de detalles con los modelos de minería de datos.  
  
|Tareas|Vínculos|  
|-----------|-----------|  
|Usar la obtención de detalles en los visores de modelos de minería de datos|[Obtención de detalles de uso de los visores de modelos](../../analysis-services/data-mining/use-drillthrough-from-the-model-viewers.md)|  
|Recuperar los datos de casos para un modelo mediante la obtención de detalles|[Profundizar en los datos de los casos de un modelo de minería de datos](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md)|  
|Habilitar la obtención de detalles en un modelo de minería de datos existente|[Habilitar obtención de detalles para un modelo de minería de datos](../../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md)|  
|Ver ejemplos de consultas de obtención de detalles para tipos de modelos concretos.|[Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)|  
|Habilitar la obtención de detalles en el Asistente para modelo de minería de datos|[Finalización del asistente &#40;Asistente para minería de datos&#41;](http://msdn.microsoft.com/library/6aef1548-35eb-42fd-ae87-63650a79eda1).|  
  
## <a name="see-also"></a>Vea también  
 [Obtención de detalles en estructuras de minería de datos](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  
