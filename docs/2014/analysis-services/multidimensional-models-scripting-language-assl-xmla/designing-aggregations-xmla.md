---
title: Diseñar agregaciones (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- statistical information [XML for Analysis]
- batches [XML for Analysis]
- aggregations [Analysis Services], XML for Analysis
- XMLA, aggregations
- queries [XMLA]
- XML for Analysis, aggregations
- iterative aggregation process [XMLA]
ms.assetid: 4dd27afa-10c7-408d-bc24-ca74217ddbcb
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 773187385538a70ed145e330eb60c648cf8f0511
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161336"
---
# <a name="designing-aggregations-xmla"></a>Diseñar agregaciones (XMLA)
  Los diseños de agregaciones están asociados a las particiones de un grupo de medida determinado para asegurar que las particiones usan la misma estructura al almacenar agregaciones. Con la misma estructura de almacenamiento para particiones le permite definir fácilmente las particiones que pueden combinarse más tarde mediante el [MergePartitions](../xmla/xml-elements-commands/mergepartitions-element-xmla.md) comando. Para obtener más información acerca de los diseños de agregaciones, vea [agregaciones y diseños de agregaciones](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md).  
  
 Para definir agregaciones para un diseño de agregaciones, puede usar el [DesignAggregations](../xmla/xml-elements-commands/designaggregations-element-xmla.md) comando XML for Analysis (XMLA). El comando `DesignAggregations` tiene propiedades que identifican el diseño de agregaciones que se usa como una referencia y definen cómo controlar el proceso de diseño basado en esa referencia. Mediante el comando `DesignAggregations` y sus propiedades, puede diseñar agregaciones de forma iterativa o por lotes y luego ver las estadísticas de diseño resultantes para evaluar el proceso de diseño.  
  
## <a name="specifying-an-aggregation-design"></a>Especificar un diseño de agregaciones  
 El [objeto](../xmla/xml-elements-properties/object-element-xmla.md) propiedad de la `DesignAggregations` comando debe contener una referencia de objeto a un diseño de agregaciones existente. La referencia de objeto contiene un identificador de la base de datos, identificador de cubo, identificador de grupo de medida e identificador de diseño de agregaciones. Si el diseño de agregaciones aún no existe, se produce un error.  
  
## <a name="controlling-the-design-process"></a>Controlar el proceso de diseño  
 Puede usar las propiedades siguientes del comando `DesignAggregations` para controlar el algoritmo que se usa para definir las agregaciones para el diseño de agregaciones:  
  
-   El [pasos](../xmla/xml-elements-properties/steps-element-xmla.md) propiedad determina cuántas iteraciones el `DesignAggregations` comando debe realizar antes de devolver el control a la aplicación cliente.  
  
-   El [tiempo](../xmla/xml-elements-properties/time-element-xmla.md) propiedad determina cuántos milisegundos del `DesignAggregations` comando debe realizar antes de devolver el control a la aplicación cliente.  
  
-   El [optimización](../xmla/xml-elements-properties/optimization-element-xmla.md) propiedad determina el porcentaje estimado de mejora del rendimiento del `DesignAggregations` comando debería intentar alcanzar. Si diseña agregaciones de forma iterativa, solo tendrá que enviar esta propiedad en el primer comando.  
  
-   El [almacenamiento](../xmla/xml-elements-properties/storage-element-xmla.md) propiedad determina la cantidad estimada de almacenamiento en disco, en bytes, utilizado por el `DesignAggregations` comando. Si diseña agregaciones de forma iterativa, solo tendrá que enviar esta propiedad en el primer comando.  
  
-   El [Materialize](../xmla/xml-elements-properties/materialize-element-xmla.md) propiedad determina si el `DesignAggregations` comando debe crear las agregaciones definidas durante el proceso de diseño. Si diseña agregaciones de forma iterativa, esta propiedad debería establecerse en false hasta que esté listo para guardar las agregaciones diseñadas. Cuando la propiedad está establecida en true, finaliza el proceso de diseño actual y las agregaciones definidas se agregan al diseño de agregaciones especificado.  
  
## <a name="specifying-queries"></a>Especificar consultas  
 El comando DesignAggregations admite el comando de optimización basada en uso incluyendo uno o más `Query` elementos en el [consultas](../xmla/xml-elements-properties/queries-element-xmla.md) propiedad. El `Queries` propiedad puede contener uno o varios [consulta](../xmla/xml-elements-properties/query-element-xmla.md) elementos. Si la propiedad `Queries` no contiene ningún elemento `Query`, el diseño de agregaciones especificado en el elemento `Object` usa una estructura predeterminada que contiene un conjunto general de agregaciones. Este conjunto general de agregaciones está diseñado para cumplir los criterios especificados en las propiedades `Optimization` y `Storage` del comando `DesignAggregations`.  
  
 Cada `Query` elemento representa una consulta de objetivo que utiliza el proceso de diseño para definir agregaciones dirigidas a las consultas utilizadas con frecuencia. Puede especificar sus propias consultas de objetivo, o puede usar la información almacenada por una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el registro de consultas para recuperar información sobre con más frecuencia utiliza las consultas. El Asistente para optimización basada en el uso utiliza el registro de la consulta para recuperar consultas de objetivo según el tiempo, uso o un usuario especificado cuando envía un comando `DesignAggregations`. Para obtener más información, consulte [ayuda F1 del Asistente para optimización basada en uso](../usage-based-optimization-wizard-f1-help.md).  
  
 Si está diseñando agregaciones de forma iterativa, solo tiene que pasar las consultas de objetivo en la primera `DesignAggregations` comando porque el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia almacena estas consultas de objetivo y las usa durante la subsiguiente `DesignAggregations` comandos. Después de incluir las consultas del objetivo en el primer comando `DesignAggregations` de un proceso iterativo, cualquier comando `DesignAggregations` posterior que contenga las consultas de objetivo en la propiedad `Queries` generará un error.  
  
 El elemento `Query` contiene un valor delimitado por comas que contiene los siguientes argumentos:  
  
 *Frequency*,*Dataset*[,*Dataset*...]  
  
 *Frecuencia*  
 Un factor de ponderación que corresponde al número de veces que se ha ejecutado con anterioridad la consulta. Si el `Query` elemento representa una consulta nueva, el *frecuencia* valor representa el factor de ponderación utilizado por el proceso de diseño para evaluar la consulta. A medida que el valor de frecuencia se vuelve mayor, el valor de ponderación que se asigna a la consulta durante el proceso de diseño va aumentando.  
  
 *Conjunto de datos*  
 Una cadena numérica que especifica qué atributos de una dimensión se van a incluir en la consulta. Esta cadena debe tener el mismo número de caracteres que el número de atributos de la dimensión. El cero (0) indica que el atributo de la posición ordinal especificada no está incluido en la consulta de la dimensión especificada, mientras que el uno (1) indica que el atributo de la posición ordinal especificada está incluido en la consulta de la dimensión especificada.  
  
 Por ejemplo, la cadena "011" haría referencia a una consulta que implicaría una dimensión con tres atributos, de los que el segundo y el tercero estarían incluidos en la consulta.  
  
> [!NOTE]  
>  Algunos atributos no se tienen en cuenta en el conjunto de datos. Para obtener más información sobre los atributos excluidos, vea [elemento Query &#40;XMLA&#41;](../xmla/xml-elements-properties/query-element-xmla.md).  
  
 Cada dimensión del grupo de medida que contiene el diseño de agregaciones está representada por un *Dataset* valor en el `Query` elemento. El orden de los valores de *Dataset* debe coincidir con el orden de las dimensiones incluidas en el grupo de medidas.  
  
## <a name="designing-aggregations-using-iterative-or-batch-processes"></a>Diseñar agregaciones mediante el proceso iterativo o proceso por lotes  
 Puede usar el comando `DesignAggregations` como parte de un proceso iterativo o proceso por lotes, dependiendo de la interactividad que requiere el proceso de diseño.  
  
### <a name="designing-aggregations-using-an-iterative-process"></a>Diseñar agregaciones mediante un proceso iterativo  
 Para diseñar agregaciones de forma iterativa, debe enviar varios comandos `DesignAggregations` para proporcionar un control exhaustivo sobre el proceso de diseño. El Asistente para diseñar agregaciones usa este mismo enfoque para proporcionar un control exhaustivo sobre el proceso de diseño. Para obtener más información, consulte [ayuda de F1 de Asistente de diseño de agregaciones](../aggregation-design-wizard-f1-help.md).  
  
> [!NOTE]  
>  Para diseñar agregaciones de forma iterativa, se requiere una sesión explícita. Para obtener más información acerca de sesiones explícitas, consulte [administrar conexiones y sesiones &#40;XMLA&#41;](managing-connections-and-sessions-xmla.md).  
  
 Para iniciar el proceso iterativo, envíe primero un comando `DesignAggregations` que contenga la información siguiente:  
  
-   Los valores de propiedad `Storage` y `Optimization` a los que va dirigido el proceso de diseño completo.  
  
-   Los valores de propiedad `Steps` y `Time` en los que se limita el primer paso del proceso de diseño.  
  
-   Si se desea una optimización basada en uso, la propiedad `Queries` que contiene las consultas de objetivo a las que va dirigido el proceso de diseño completo.  
  
-   La propiedad `Materialize` está establecida en false. Establecer esta propiedad en false indica que el proceso de diseño no guarda las agregaciones definidas en el diseño de agregaciones una vez completado el comando.  
  
 Cuando finaliza el primer comando `DesignAggregations`, éste devuelve un conjunto de filas que contiene las estadísticas de diseño. Puede evaluar estas estadísticas de diseño para determinar si el proceso de diseño debe continuar o si ha finalizado. Si el proceso debe continuar, entonces envíe otro comando `DesignAggregations` que contenga los valores `Steps` y `Time` con los que se limita este paso del proceso de diseño. Evalúe las estadísticas resultantes y, a continuación, determine si el proceso de diseño debe continuar. Este proceso iterativo de enviar comandos `DesignAggregations` y evaluar los resultados continúa hasta que alcance sus objetivos y tenga un conjunto de agregaciones adecuado y definido.  
  
 Cuando haya obtenido el conjunto de agregaciones que desea, envíe un último comando `DesignAggregations`. Este último comando `DesignAggregations` debe tener su propiedad `Steps` establecida en 1 y su propiedad `Materialize` establecidas en true. Al usar estos valores, este último comando `DesignAggregations` completa el proceso del diseño y guarda la agregación definida en el diseño de agregaciones.  
  
### <a name="designing-aggregations-using-a-batch-process"></a>Diseñar agregaciones mediante un proceso por lotes  
 También puede diseñar agregaciones en un proceso por lotes enviando un único comando `DesignAggregations` que contiene los valores de propiedad `Steps`, `Time`, `Storage` y `Optimization` a los que el proceso de diseño completo va dirigido y se limita. Si desea una optimización basada en uso, las consultas de objetivo a las que se dirige el proceso de diseño deberían también estar incluidas en la propiedad `Queries`. Asegúrese también de que la propiedad `Materialize` está establecida en true, para que el proceso de diseño guarde las agregaciones definidas en el diseño de agregaciones cuando finaliza el comando.  
  
 Puede diseñar agregaciones mediante un proceso por lotes en una sesión tanto implícita como explícita. Para obtener más información acerca de las sesiones implícitas y explícitas, consulte [administrar conexiones y sesiones &#40;XMLA&#41;](managing-connections-and-sessions-xmla.md).  
  
## <a name="returning-design-statistics"></a>Devolver estadísticas de diseño  
 Cuando el comando `DesignAggregations` devuelve el control a la aplicación cliente, el comando devuelve un conjunto de filas que contiene una fila única que representa las estadísticas de diseño para el comando. El conjunto de filas contiene las columnas que se muestran en la tabla siguiente.  
  
|columna|Data type|Descripción|  
|------------|---------------|-----------------|  
|Pasos|Integer|El número de pasos que realiza el comando antes de devolver el control a la aplicación cliente.|  
|Time|Entero largo|El número de milisegundos que tarda el comando antes de devolver el control a la aplicación cliente.|  
|Optimization|Doble|El porcentaje estimado de mejora del rendimiento que alcanza el comando antes de devolver el control a la aplicación cliente.|  
|Storage|Entero largo|El número estimado de bytes que toma el comando antes de devolver el control a la aplicación cliente.|  
|Agregaciones|Entero largo|El número de agregaciones definido por el comando antes de devolver el control a la aplicación cliente.|  
|LastStep|Boolean|Indica si los datos en el conjunto de filas representan el último paso del proceso de diseño. Si la propiedad `Materialize` del comando está establecida en true, el valor de esta columna está establecido en true.|  
  
 Puede usar las estadísticas de diseño contenidas en el conjunto de filas que se devuelve después de cada comando `DesignAggregations` en ambos diseños, iterativo y por lotes. En diseño iterativo, puede usar estadísticas de diseño para determinar y mostrar el progreso. Cuando diseña agregaciones por lotes, puede usar estadísticas de diseño para determinar el número de agregaciones que crea el comando.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollo con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
