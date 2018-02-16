---
title: Particiones en modelos multidimensionales | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 26e01dc7-fa49-4b1f-99eb-7799d1b4dcd2
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6984e77d1969db95ac8b8659ba841085ce7ef7c8
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="partitions-in-multidimensional-models"></a>Particiones en modelos multidimensionales
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una *partición* proporciona el almacenamiento físico de los datos de hechos cargados en un grupo de medida. Se crea automáticamente una sola partición para cada grupo de medida, aunque es frecuente crear particiones adicionales que segmenten aún más los datos, lo que produce un procesamiento más eficiente y un rendimiento de las consultas más rápido.  
  
 El procesamiento es más eficaz porque las particiones se pueden procesar independientemente y en paralelo, en uno o más servidores. Las consultas se ejecutan más rápido porque se puede configurar cada partición para que tenga modos de almacenamiento y optimizaciones de agregación que reducen los tiempos de respuesta. Por ejemplo, elegir el almacenamiento MOLAP para las particiones que contienen datos más recientes suele ser más rápido que ROLAP. Del mismo modo, si se crean particiones por fecha, las particiones que contienen los datos más recientes pueden tener más optimizaciones que las particiones que contienen datos antiguos a los que se obtiene acceso con menos frecuencia. Tenga en cuenta que el diseño de almacenamiento y agregación por partición tendrá un impacto negativo sobre las operaciones de mezcla futuras. Debe tener en cuenta si la mezcla es un componente esencial de la estrategia de administración de particiones antes de optimizar las particiones individuales.  
  
> [!NOTE]  
>  Se admiten varias particiones en las ediciones Business Intelligence y Enterprise. La edición Standard no admite varias particiones. Para obtener más información, vea [Características compatibles con las ediciones de SQL Server 2016](../../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).  
  
## <a name="important-considerations-when-designing-a-partitioning-strategy"></a>Consideraciones importantes a la hora de diseñar una estrategia de particiones  
 La integridad de los datos de un cubo se basa en los datos que se distribuyen entre las particiones del cubo de forma que no se duplique ningún dato entre ellas. Cuando se resumen los datos de las particiones, los elementos de datos que estén presentes en más de una partición se resumirán como si fueran elementos de datos diferentes. Esto puede dar lugar a que se presenten resúmenes incorrectos y datos erróneos al usuario final. Por ejemplo, si una transacción de ventas para el producto X está duplicada en las tablas de hechos para dos particiones, los resúmenes de las ventas de dicho producto pueden incluir una dicha transacción por partida doble.  
  
 Se pueden mezclar particiones; puede usar esta característica en su estrategia de actualización de datos y almacenamiento global. Solo se pueden mezclar particiones si tienen el mismo modo de almacenamiento y el mismo diseño de agregaciones. Si desea crear particiones que sean candidatas a una combinación posterior, copie el diseño de agregaciones de otra partición al crearlas. También puede modificar una partición una vez creada para copiar el diseño de agregaciones de otra partición. Asimismo, la combinación de particiones se debe realizar cuidadosamente para evitar la duplicación de datos en la partición resultante, lo que podría provocar que haya datos incorrectos en el cubo.  
  
## <a name="local-partitions"></a>Particiones locales  
 Las particiones locales son particiones que se definen, procesan y almacenan en un servidor. Si tiene grandes grupos de medida en un cubo, es posible que desee crear particiones de forma que el procesamiento se realice en paralelo en todas las particiones. La ventaja es que el procesamiento en paralelo ofrece una ejecución más rápida. Puesto que el trabajo de procesamiento de una partición no tiene que finalizar antes de que otro empiece, pueden ejecutarse en paralelo. Para obtener más información, vea [Create and Manage a Local Partition &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md).  
  
## <a name="remote-partitions"></a>Particiones remotas  
 Las particiones remotas son particiones que se definen en un servidor,  pero se procesan y almacenan en otro. Utilice particiones remotas si desea distribuir el almacenamiento de los datos y metadatos en varios servidores. En general, cuando se pasa del desarrollo a la producción, el tamaño de los datos bajo análisis se multiplica. Con cantidades de datos tan grandes, una posible alternativa es distribuirlos en varios equipos. Esto se lleva a cabo no solo porque un equipo no podría contener todos los datos, sino también para que el procesamiento de los datos se realice en paralelo en varios equipos. Para obtener más información, vea [Create and Manage a Remote Partition &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md).  
  
## <a name="aggregations"></a>Agregaciones  
 Las agregaciones son resúmenes precalculados de datos de cubo que permiten a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporcionar respuestas de consulta rápidas. Puede controlar el número de agregaciones creadas para un grupo de medida si establece límites de almacenamiento, mejoras de rendimiento o detiene arbitrariamente el proceso de generación de agregaciones después de que se haya estado ejecutando durante algún tiempo. Un número mayor de agregaciones no es necesariamente mejor. Cada agregación nueva supone un costo, tanto en términos de espacio en disco como en tiempo de procesamiento. Se recomienda crear agregaciones para lograr una mejora del rendimiento del treinta por ciento e incrementar después ese número solo si las pruebas o la experiencia lo garantiza. Para obtener más información, vea [Diseñar agregaciones &#40;Analysis Services - Multidimensional&#41;](../../analysis-services/multidimensional-models/designing-aggregations-analysis-services-multidimensional.md).  
  
## <a name="partition-merging-and-editing"></a>Mezclar y editar particiones  
 Si dos particiones utilizan el mismo diseño de agregaciones, puede mezclarlas en una sola. Por ejemplo, si dispone de una dimensión de inventario con particiones por meses, al final de cada mes puede mezclar esa partición mensual con la partición anual existente. De esta forma, la partición del mes actual se puede procesar y analizar rápidamente, en tanto que el resto de los meses del año solamente tendrá que procesarse de nuevo cuando se realice la mezcla. Este reproceso requiere un mayor tiempo de procesamiento y puede ejecutarse con menos frecuencia. Para obtener más información sobre la administración del proceso de mezcla de particiones, vea [Merge Partitions in Analysis Services &#40;SSAS - Multidimensional&#41;](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md). Para editar las particiones del cubo mediante el **particiones** pestaña Diseñador de cubos, vea [editar o eliminar particiones &#40; Analysis Services - Multidimensional &#41; ](../../analysis-services/multidimensional-models/edit-or-delete-partitions-analyisis-services-multidimensional.md).  
  
## <a name="related-topics"></a>Temas relacionados  
  
|Tema|Description|  
|-----------|-----------------|  
|[Crear y administrar una partición Local &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)|Contiene información sobre cómo crear particiones de los datos usando filtros o tablas de hechos diferentes sin duplicar los datos.|  
|[Almacenamiento de particiones del conjunto &#40; Analysis Services - Multidimensional &#41;](../../analysis-services/multidimensional-models/set-partition-storage-analysis-services-multidimensional.md)|Describe cómo configurar el almacenamiento para las particiones.|  
|[Editar o eliminar particiones &#40; Analysis Services - Multidimensional &#41;](../../analysis-services/multidimensional-models/edit-or-delete-partitions-analyisis-services-multidimensional.md)|Describe cómo ver y modificar las particiones.|  
|[Mezclar particiones en Analysis Services &#40; SSAS - Multidimensional &#41;](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)|Contiene información sobre cómo mezclar particiones que tienen distintas tablas de hechos o distintos segmentos de datos sin duplicar los datos.|  
|[Establecer la reescritura de particiones](../../analysis-services/multidimensional-models/set-partition-writeback.md)|Proporciona instrucciones sobre cómo habilitar una partición para escritura.|  
|[Crear y administrar una partición remota &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)|Describe cómo crear y administrar una partición remota.|  
  
  
