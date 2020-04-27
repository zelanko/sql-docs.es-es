---
title: Particiones (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- incremental updates [Analysis Services]
- data sources [Analysis Services], partitions
- data storage [Analysis Services]
- aggregations [Analysis Services], partitions
- OLAP objects [Analysis Services], partitions
- storing data [Analysis Services], partitions
- partitions [Analysis Services], about partitions
- cubes [Analysis Services], partitions
- partitions [Analysis Services]
- remote partitions [Analysis Services]
- measure groups [Analysis Services], partitions
ms.assetid: cd10ad00-468c-4d49-9f8d-873494d04b4f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 47a7b4c2b11a6d17a52af20aef71ee13863ea29c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62702619"
---
# <a name="partitions-analysis-services---multidimensional-data"></a>Particiones (Analysis Services - Datos multidimensionales)
  Una partición es un contenedor para una parte de los datos del grupo de medidas. Las particiones no se ven de las consultas MDX; todas las consultas reflejan el contenido completo del grupo de medidas, sin tener en cuenta cuántas particiones se definen para el grupo de medidas. Los enlaces de consultas de la partición, y la expresión de segmentación, definen el contenido de los datos de una partición.  
  
 Un objeto <xref:Microsoft.AnalysisServices.Partition> simple se crea con la información básica, la definición de segmentación y el diseño de agregaciones, entre otros. La información básica incluye el nombre de la partición, el modo de almacenamiento, el modo de procesamiento y otros aspectos. La definición de la segmentación es una expresión MDX que especifica una tupla o un conjunto. La definición de la segmentación tiene las mismas restricciones que la función MDX StrToSet. Junto con el parámetro CONSTRAINED, la definición de la segmentación puede usar la dimensión, la jerarquía, el nivel y los nombres de miembros, las claves, los nombres únicos u otros objetos con nombre del cubo, pero no puede usar funciones MDX. El diseño de agregaciones es una colección de definiciones de agregaciones que se pueden compartir en varias particiones. El valor predeterminado se toma del diseño de agregaciones del cubo primario.  
  
 Utiliza [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] las particiones para administrar y almacenar los datos y las agregaciones de un grupo de medida en un cubo. Cada grupo de medida tiene al menos una partición; esta partición se crea al definir el grupo de medida. Cuando se crea una partición para un grupo de medida, ésta se agrega al conjunto de particiones que ya existen para dicho grupo. El grupo de medida refleja los datos combinados contenidos en todas sus particiones. Esto implica que debe asegurarse de que los datos de una partición de un grupo de medida sean distintos a los datos de cualquier otra partición del grupo de medida a fin de garantizar que los datos no queden reflejados en el grupo de medida más de una vez. La partición original de un grupo de medida se basa en una sola tabla de hechos en la vista del origen de datos del cubo. Cuando hay varias particiones para un grupo de medida, cada partición puede hacer referencia a una tabla diferente de la vista del origen de datos o del origen de datos relacionales subyacente para el cubo. Varias particiones de un grupo de medida pueden hacer referencia a la misma tabla si cada partición se restringe a diferentes filas de la tabla.  
  
 Las particiones son un medio eficaz y flexible de administrar cubos, especialmente los cubos grandes. Por ejemplo, un cubo que contenga información de ventas puede contar con una partición para los datos de los años anteriores y, además, particiones para cada trimestre del año en curso. Cuando se agrega información actual al cubo, solo es necesario procesar la partición del trimestre actual. El procesamiento de una menor cantidad de datos mejorará el rendimiento del procesamiento, ya que reduce el tiempo necesario. Al final del año se pueden unir las cuatro particiones trimestrales para formar una sola de todo el año y se puede crear una nueva partición para el primer trimestre del año siguiente. Además, el proceso de creación de esta nueva partición se puede automatizar como parte de los procedimientos de carga de almacenamiento de datos y procesamiento de cubos.  
  
 Las particiones no son visibles para los usuarios empresariales del cubo. Sin embargo, los administradores pueden configurar, agregar o quitar particiones. Cada partición se almacena en un conjunto de archivos independiente. Los datos agregados de cada partición pueden almacenarse en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] donde se define la partición, en otra instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]o en el mismo origen de datos que se usa para suministrar los datos de origen de la partición. Las particiones permiten que los datos de origen y los datos agregados de un cubo se distribuyan en varios discos duros y en varios servidores. Para un cubo de tamaño moderado a grande, las particiones pueden mejorar en gran medida el rendimiento de las consultas y la carga, y facilitar el mantenimiento del cubo. Para más información sobre las particiones remotas, vea [Particiones remotas](partitions-remote-partitions.md).  
  
 El modo de almacenamiento de cada partición puede configurarse independientemente de otras particiones en el grupo de medida. Las particiones pueden almacenarse mediante combinaciones de opciones para la ubicación de datos de origen, el modo de almacenamiento, el almacenamiento en caché automático y el diseño de agregaciones. Las opciones de almacenamiento en caché automático y OLAP en tiempo real permiten equilibrar la velocidad de las consultas con la latencia cuando se diseña una partición. Las opciones de almacenamiento también se pueden aplicar a dimensiones relacionadas y hechos de un grupo de medida. Esta flexibilidad permite diseñar estrategias de almacenamiento de cubos adecuadas para sus necesidades. Para obtener más información, consulte [procesamiento y modos de almacenamiento de particiones](partitions-partition-storage-modes-and-processing.md), [agregaciones y diseños de agregaciones](aggregations-and-aggregation-designs.md) y [almacenamiento en caché automático &#40;particiones&#41;](partitions-proactive-caching.md).  
  
## <a name="partition-structure"></a>Estructura de una partición  
 La estructura de una partición debe coincidir con la de su grupo de medida, es decir, las medidas que definen el grupo de medida también se deben definir en la partición, junto con todas las dimensiones relacionadas. Por lo tanto, cuando se crea una partición, ésta hereda automáticamente el mismo conjunto de medidas y dimensiones relacionadas que se definieron para el grupo de medida.  
  
 Sin embargo, cada partición de un grupo de medida puede tener una tabla de hechos distinta que, a su vez, puede proceder de distintos orígenes de datos. Cuando las distintas particiones de un grupo de medida tienen distintas tablas de hechos, las tablas deben ser bastante similares para mantener la estructura del grupo de medida, lo que significa que la consulta de procesamiento devuelve las mismas columnas y los mismos tipos de datos para todas las tablas de hechos de todas las particiones.  
  
 Cuando tablas de hechos para diferentes particiones provienen de diferentes orígenes de datos, las tablas de origen para las dimensiones relacionadas, así como las tablas de hechos intermedias, deben estar presentes en todos los orígenes de datos y tener la misma estructura en todas las bases de datos. Además, todas las columnas de las tablas de dimensiones que se utilizan para definir atributos de dimensiones de cubos relacionadas con el grupo de medida deben estar presentes en todos los orígenes de datos. No es necesario definir todas las combinaciones entre la tabla de origen de una partición y una tabla de dimensiones relacionada si la tabla de origen de la partición tiene idéntica estructura que la tabla de origen para el grupo de medida.  
  
 Las columnas que no se utilizan para definir medidas en el grupo de medida pueden estar presentes en algunas tablas de hechos y ausentes en otras. De forma similar, las columnas que no se utilizan para definir atributos en las tablas de dimensiones relacionadas pueden estar presentes en algunas bases de datos y ausentes en otras. Las tablas que no se utilizan en tablas de hechos ni en tablas de dimensiones relacionadas pueden estar presentes en algunas bases de datos y ausentes en otras.  
  
## <a name="data-sources-and-partition-storage"></a>Orígenes de datos y almacenamiento de particiones  
 Una partición se basa en una tabla o vista de un origen de datos, o bien, en una tabla o consulta con nombre de una vista del origen de datos. La ubicación donde se almacenan los datos de particiones se define mediante los enlaces de orígenes de datos. Normalmente se puede crear una partición de un grupo de medida en sentido horizontal o vertical:  
  
-   En un grupo de medida con particiones horizontales, cada partición de un grupo de medida se basa en una tabla independiente. Este tipo de particiones es adecuado cuando los datos están separados en varias tablas. Por ejemplo, algunas bases de datos relacionales tienen una tabla diferente para los datos de cada mes.  
  
-   En un grupo de medida con particiones verticales, un grupo de medida se basa en una sola tabla y cada partición se basa en una consulta del sistema de origen que filtra los datos para la partición. Por ejemplo, si una tabla contiene varios datos de meses, el grupo de medida podría seguir con particiones por mes aplicando una cláusula WHERE de Transact-SQL que devuelve los datos de un mes independiente para cada partición.  
  
 Cada partición tiene una configuración de almacenamiento que determina si los datos y agregaciones de la partición se almacenan en la instancia local de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o en una partición remota que utiliza otra instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La configuración de almacenamiento también puede especificar el modo de almacenamiento y si el almacenamiento en caché automático se usa para controlar la latencia de una partición. Para obtener más información, consulte el [procesamiento y los modos de almacenamiento de particiones](partitions-partition-storage-modes-and-processing.md), el [almacenamiento en caché automático &#40;las particiones&#41;](partitions-proactive-caching.md)y las [particiones remotas](partitions-remote-partitions.md).  
  
## <a name="incremental-updates"></a>Actualizaciones incrementales  
 Cuando se crean y administran particiones en grupos de medida con varias particiones, es necesario tomar precauciones especiales para garantizar que los datos del cubo sean exactos. Aunque estas precauciones no suelen aplicarse a los grupos de medida con una sola partición, sí se aplican cuando se actualizan incrementalmente las particiones. Al actualizar incrementalmente una partición, se crea una partición temporal con una estructura idéntica a la de la partición de origen. La partición temporal se procesa y luego se mezcla con la partición de origen. Por lo tanto, debe asegurarse de que la consulta de procesamiento que llena la partición temporal no duplica ningún dato que ya esté en una partición existente.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar propiedades de medidas](../multidimensional-models/configure-measure-properties.md)   
 [Cubos en modelos multidimensionales](../multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
