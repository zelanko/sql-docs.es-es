---
title: Modos de almacenamiento y procesamiento de partición | Microsoft Docs
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
- storage [Analysis Services], partitions
- hybrid OLAP
- data storage [Analysis Services]
- relational OLAP
- multidimensional OLAP
- partitions [Analysis Services], storage
- storing data [Analysis Services], partitions
- HOLAP
- MOLAP
- ROLAP
ms.assetid: 86d17547-a0b6-47ac-876c-d7a5b15ac327
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 70214fb48ffa66fdfeca56eccebdb335c11a214f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273441"
---
# <a name="partition-storage-modes-and-processing"></a>Procesamiento y modos de almacenamiento de particiones
  El modo de almacenamiento de una partición afecta al rendimiento de las consultas y el procesamiento, a los requisitos de almacenamiento y a las ubicaciones de almacenamiento de la partición y de su grupo de medida y cubo primario.  La elección del modo de almacenamiento afecta también a las opciones de procesamiento.  
  
 Una partición puede utilizar uno de estos tres modos de almacenamiento básicos:  
  
-   OLAP multidimensional (MOLAP)  
  
-   OLAP relacional (ROLAP)  
  
-   OLAP híbrido (HOLAP)  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite los tres modos de almacenamiento básico. También admite el almacenamiento en caché automático, que permite combinar las características de almacenamiento ROLAP y MOLAP para mejorar la disponibilidad de los datos y el rendimiento de las consultas. Para más información, vea [Almacenamiento en caché automático &#40;Particiones&#41;](partitions-proactive-caching.md).  
  
## <a name="molap"></a>MOLAP  
 El modo de almacenamiento MOLAP da lugar a que las agregaciones de la partición y una copia de sus datos de origen se almacenen en una estructura multidimensional en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Esta estructura MOLAP está muy optimizada para maximizar el rendimiento de las consultas. La ubicación de almacenamiento puede estar en el equipo en donde se define la partición o en otro equipo que ejecute [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Dado que una copia de los datos de origen reside en la estructura multidimensional, las consultas se pueden resolver sin necesidad de obtener acceso a los datos de origen de la partición. Si se utilizan agregaciones, los tiempos de respuesta a las consultas pueden disminuir notablemente. Los datos de la estructura MOLAP de la partición están tan actualizados como el procesamiento más reciente de la misma.  
  
 A medida que cambian los datos de origen, los objetos con almacenamiento MOLAP se deben procesar periódicamente para incorporar estos cambios y ponerlos a disposición de los usuarios. El procesamiento actualiza los datos en la estructura MOLAP, ya sea completamente o incrementalmente. El tiempo entre un procesamiento y el siguiente crea un periodo de latencia durante el cual los datos de los objetos OLAP podrían no coincidir con los datos de origen. Es posible actualizar los objetos en almacenamiento MOLAP completamente o incrementalmente sin dejar sin conexión la partición o el cubo. Sin embargo, hay casos en que puede ser necesario dejar sin conexión un cubo para procesar algunos cambios estructurales de objetos OLAP. El tiempo de inactividad requerido para actualizar el almacenamiento MOLAP se puede minimizar actualizando y procesando cubos en un servidor de ensayo y utilizando la sincronización de bases de datos para copiar los objetos procesados en el servidor de producción. También se puede usar el almacenamiento en caché automático para minimizar la latencia y maximizar la disponibilidad, a la vez que se mantiene gran parte de las ventajas de rendimiento del almacenamiento MOLAP. Para obtener más información, consulte [almacenamiento en caché automático &#40;particiones&#41;](partitions-proactive-caching.md), [Synchronize Analysis Services Databases](../multidimensional-models/synchronize-analysis-services-databases.md), y [procesamiento de objetos de modelo Multidimensional](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
## <a name="rolap"></a>ROLAP  
 El modo de almacenamiento ROLAP hace que las agregaciones de la partición se almacenen en vistas indizadas de la base de datos relacional que se especificó en el origen de datos de la partición. A diferencia del modo de almacenamiento MOLAP, ROLAP no hace que se almacene una copia de los datos del origen en las carpetas de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. En su lugar, cuando no se pueden derivar los resultados de la caché de consultas, se utilizan las vistas indizadas del origen de datos para responder a las consultas. La respuesta a las consultas suele ser más lenta con el almacenamiento ROLAP que con los modos de almacenamiento MOLAP o HOLAP. El tiempo de procesamiento también suele ser más lento con ROLAP. No obstante, ROLAP permite a los usuarios ver los datos en tiempo real y ahorrar espacio de almacenamiento al trabajar con conjuntos de datos grandes a los que no se suele consultar con frecuencia, como datos puramente históricos.  
  
> [!NOTE]  
>  Cuando se usa ROLAP, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede devolver información incorrecta relacionada con el miembro desconocido si se combina una combinación con una cláusula GROUP BY. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] elimina errores de integridad relacional, en lugar de devolver el valor del miembro desconocido.  
  
 Si una partición utiliza el modo de almacenamiento ROLAP y sus datos de origen se almacenan en [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] intentará crear vistas indizadas para contener las agregaciones de la partición. Si [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no puede crear vistas indizadas, no creará tablas de agregaciones. Aunque [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] controla los requisitos de la sesión para crear vistas indizadas en [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], para que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cree vistas indizadas de agregaciones es necesario que la partición ROLAP y las tablas de su esquema cumplan con las siguientes condiciones:  
  
-   La partición no puede contener medidas que utilicen las funciones de agregado `Min` o `Max`.  
  
-   Cada tabla del esquema de la partición ROLAP solo debe utilizarse una vez. Por ejemplo, el esquema no puede contener [dbo].[address] AS "Customer Address" ni [dbo].[address] AS "SalesRep Address".  
  
-   Cada tabla debe ser una tabla, no una vista.  
  
-   Todos los nombres de tablas del esquema de la partición deben estar calificados con el nombre del propietario [dbo].[customer].  
  
-   Todas las tablas del esquema de la partición deben tener el mismo propietario; por ejemplo, no se puede tener una cláusula FROM que haga referencia a las tablas [tk].[customer], [john].[store] y [dave].[sales_fact_2004].  
  
-   Las columnas de origen de las medidas de la partición no deben admitir valores NULL.  
  
-   Todas las tablas utilizadas en la vista deben crearse con las siguientes opciones activadas:  
  
    -   ANSI_NULLS  
  
    -   QUOTED_IDENTIFIER  
  
-   En [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], el tamaño total de la clave de índice no puede superar los 900 bytes. [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] impondrá esta condición basándose en las columnas de clave de longitud fija cuando se procesa la instrucción CREATE INDEX. Sin embargo, si hay columnas de longitud variable en la clave de índice, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] también impondrá esta condición para cada actualización de las tablas base. Dado que las agregaciones diferentes tienen definiciones de vistas distintas, el procesamiento ROLAP mediante vistas indizadas puede realizarse correcta o incorrectamente, dependiendo del diseño de las agregaciones.  
  
-   La sesión que crea la vista indizada debe tener activadas las siguientes opciones: ARITHABORT, CONCAT_NULL_YEILDS_NULL, QUOTED_IDENTIFIER, ANSI_NULLS, ANSI_PADDING y ANSI_WARNING. Esta configuración puede crearse en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   La sesión que crea la vista indizada debe tener desactivada la siguiente opción: NUMERIC_ROUNDABORT. Esta configuración puede crearse en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="holap"></a>HOLAP  
 El modo de almacenamiento HOLAP combina atributos de los modos MOLAP y ROLAP. Al igual que MOLAP, HOLAP hace que las agregaciones de la partición se almacenen en una estructura multidimensional en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia. HOLAP no hace que se almacene una copia de los datos de origen. HOLAP es el equivalente de MOLAP para las consultas que solo tienen acceso a los datos de resumen de las agregaciones de una partición. Las consultas con acceso a los datos de origen como, por ejemplo, la obtención de detalles para una celda de un cubo atómico sin datos de agregación, deben recuperar datos de la base de datos relacional y no serán tan rápidas como lo serían si los datos de origen se hubieran almacenado en la estructura MOLAP. Con el modo de almacenamiento HOLAP, los usuarios suelen experimentar notables diferencias en cuanto a los tiempos de las consultas según si la consulta se puede resolver desde la caché o las agregaciones frente a los propios datos de origen.  
  
 Las particiones almacenadas como HOLAP son más pequeñas que sus equivalentes MOLAP dado que no contienen datos de origen y responden más rápidamente que las particiones ROLAP a las consultas que implican datos de resumen. El modo de almacenamiento HOLAP suele ser más adecuado para particiones en cubos que requieren una respuesta de consultas rápida para resúmenes basados en una gran cantidad de datos de origen. No obstante, si los usuarios generan consultas que deben utilizar datos del nivel hoja (por ejemplo, para calcular valores medios), MOLAP suele ser una opción mejor.  
  
## <a name="see-also"></a>Vea también  
 [Almacenamiento en caché automático &#40;particiones&#41;](partitions-proactive-caching.md)   
 [Sincronizar bases de datos de Analysis Services](../multidimensional-models/synchronize-analysis-services-databases.md)   
 [Las particiones &#40;Analysis Services - datos multidimensionales&#41;](partitions-analysis-services-multidimensional-data.md)  
  
  
