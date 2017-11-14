---
title: Definir particiones de modelos de DirectQuery (SSAS Tabular) | Documentos de Microsoft
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5f179ba9-6efb-46ae-90e5-945bbfddb719
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd4570e403d7a7ffd72600efedf7023da8661d98
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="define-partitions-in-directquery-models"></a>Definición de particiones en los modelos DirectQuery

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  En esta sección se explica cómo se utilizan las particiones en los modelos DirectQuery. Para obtener información general sobre las particiones en los modelos tabulares, vea [Particiones &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md).  
  
> [!NOTE]  
>  Aunque una tabla puede tener varias particiones, en el modo DirectQuery, solo una de ellas puede designarse para uso en la ejecución de consultas. El requisito de una sola partición se aplica a los modelos DirectQuery en todos los niveles de compatibilidad.  
  
## <a name="using-partitions-in-directquery-mode"></a>El uso de particiones en el modo DirectQuery  
 Para cada tabla, debe especificar una única partición para utilizar como origen de datos de DirectQuery.  De forma predeterminada, si existen varias particiones, al cambiar el modelo para habilitar el modo DirectQuery, la primera partición que se creó en la tabla se marcará como la partición DirectQuery. Puede cambiar este comportamiento posteriormente mediante el Administrador de particiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 ¿Por qué permitir únicamente una sola partición en el modo DirectQuery?  
  
 En los modelos tabulares (al igual que en los modelos OLAP), las particiones de una tabla se definen mediante consultas SQL. El desarrollador que crea la definición de la partición es el responsable de garantizar que las particiones no superpongan. Analysis Services no comprueba si los registros pertenecen a una o a varias particiones.  
  
 Las particiones de un modelo tabular almacenado en caché se comportan de la misma manera. Si se utiliza un modelo en memoria, las fórmulas DAX se evalúan para cada partición mientras se obtiene acceso a la caché, y se combinan los resultados. Sin embargo, cuando un modelo tabular utiliza el modo DirectQuery, no se puede evaluar varias particiones, combinar los resultados y convertir todo esto en una instrucción SQL para enviarla al almacén de datos relacional. Esto podría ocasionar una pérdida inaceptable de rendimiento, así como posibles imprecisiones a medida que se agregan los resultados.  
  
 Por lo tanto, para las consultas respondidas en modo DirectQuery, el servidor usa una única partición que se ha marcado como partición principal para el acceso de DirectQuery, denominada *partición DirectQuery*.  La consulta SQL especificada en la definición de esta partición define el conjunto completo de datos que pueden usarse para responder consultas en el modo DirectQuery.  
  
 Si no define de forma explícita una partición, el motor simplemente emite una consulta SQL al origen de datos relacional completo, realiza las operaciones basadas en conjuntos dictadas por la fórmula DAX y devuelve los resultados de la consulta.  
  
  
## <a name="change-a-directquery-partition"></a>Cambio de una partición DirectQuery  
 Dado que únicamente se puede designar una partición de una tabla como la partición DirectQuery, Analysis Services utiliza de forma predeterminada la primera partición que se creó en la tabla. Durante la creación del proyecto de modelos, puede cambiar la partición DirectQuery utilizando el cuadro de diálogo Administrador de particiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para los modelos implementados, puede cambiar la partición DirectQuery utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="change-the-directquery-partition-for-a-tabular-model-project"></a>Cambiar la partición de DirectQuery para un proyecto de modelos tabular  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], en el diseñador de modelos, haga clic en la tabla (pestaña) que contiene la tabla con particiones.  
  
2.  Haga clic en el menú **Tabla** y en **Particiones**.  
  
3.  En el **Administrador de particiones**, la partición asignada como la partición DirectQuery actual incluye el prefijo **(DirectQuery)** en el nombre de partición.  
  
     Seleccione otra partición en la lista **Particiones** y haga clic en **Establecer como DirectQuery**. El botón **Establecer como DirectQuery** no está habilitado si está seleccionada la partición DirectQuery actual, y no está visible si el modelo no se ha habilitado para el modo de consulta directa.  
  
4.  Si es necesario, cambie las opciones de procesamiento y, a continuación, haga clic en **Aceptar**.  
  
#### <a name="change-the-directquery-partition-for-a-deployed-tabular-model"></a>Cambiar la partición de DirectQuery para un modelo tabular implementado  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra la base de datos del modelo en el Explorador de objetos.  
  
2.  Expanda el nodo **Tablas** , haga clic con el botón derecho en la tabla con particiones y, después, seleccione **Particiones**.  
  
     La partición designada para su uso con el modo DirectQuery tiene el prefijo (DirectQuery) en el nombre de partición.  
  
3.  Para cambiar a una partición diferente, haga clic en el icono **Consulta directa** de la barra de herramientas para abrir el cuadro de diálogo **Establecer partición DirectQuery** . El icono de la barra de herramientas de DirectQuery no está disponible en los modelos no habilitados para la consulta directa.  
  
4.  Elija una partición diferente en la lista desplegable **Nombre de partición** y, a continuación, cambie las opciones de procesamiento de la partición si es necesario.  
  
## <a name="partitions-in-cached-models-and-in-directquery-models"></a>Particiones de modelos almacenados en caché y modelos DirectQuery  
 Al configurar una partición DirectQuery, debe especificar las opciones de procesamiento para la partición.  
  
 Hay dos opciones de procesamiento para la partición DirectQuery. Para establecer esta propiedad, use el **Administrador de particiones** en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y seleccione la propiedad **Opción de procesamiento** . En la tabla siguiente se muestran los valores de esta propiedad y se describen los efectos de cada valor cuando se combinan con la propiedad DirectQueryUsage en la cadena de conexión:  
  
|Propiedad**Cadena de conexión** |Propiedad**Opción de procesamiento** |Notas|  
|------------------------------------|------------------------------------|-----------|  
|DirectQuery|No procesar nunca esta partición|Cuando el modelo utiliza Solo DirectQuery, el procesamiento no es necesario nunca.<br /><br /> En los modelos híbridos, es posible configurar la partición DirectQuery para que no se procese nunca. Por ejemplo, si está trabajando con un conjunto de datos muy grande y no desea que los resultados completos se agreguen a la memoria caché, puede especificar que la partición DirectQuery incluya la unión de los resultados para el resto de particiones de la tabla y no procesar nunca dicha unión. Las consultas dirigidas al origen relacional no se verán afectadas, y las consultas en los datos en caché combinarán datos del resto de particiones|  
|DataView=Sample<br /><br /> Se aplica a modelos tabulares mediante vistas de datos de ejemplo|Permitir procesar la partición|Si el modelo utiliza datos de ejemplo, puede procesar la tabla para que devuelva un conjunto de datos filtrado que proporciona indicaciones visuales durante el diseño del modelo.|  
|DirectQueryUsage=InMemory With DirectQuery<br /><br /> Se aplica a los modelos Tabular 1100 o 1103 que se ejecutan en una combinación de en memoria y el modo DirectQuery.|Permitir procesar la partición|Si el modelo utiliza el modo híbrido, debe usar la misma partición para las consultas en memoria y las consultas en memoria y en el origen de datos de DirectQuery.|  
  
## <a name="see-also"></a>Vea también  
 [Particiones &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  

