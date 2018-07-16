---
title: Requisitos y consideraciones para el análisis de servicios de implementación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- memory [Analysis Services]
- scalability [Analysis Services]
- space [Analysis Services]
- Analysis Services deployments, requirements
- deploying [Analysis Services], requirements
- disk space [Analysis Services]
- requirements [Analysis Services]
- processors [Analysis Services]
- system requirements [Analysis Services]
- availability [Analysis Services]
ms.assetid: ef1387a5-5137-4ef4-b731-fec347e5f5ed
caps.latest.revision: 24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e3cb9b81c5125f8d4f0e9dd2e0760a072d655f6e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37247775"
---
# <a name="requirements-and-considerations-for-analysis-services-deployment"></a>Requisitos y consideraciones para la implementación de Analysis Services
  El rendimiento y la disponibilidad de una solución dependen de muchos factores, como son las capacidades del hardware subyacente, la topología de la implementación del servidor, las características de la solución (por ejemplo, si tiene particiones distribuidas en varios servidores o usa el almacenamiento ROLAP que requiere acceso directo al motor relacional), los contratos de nivel de servicio y la complejidad del modelo de datos.  
  
## <a name="memory-and-processor-requirements"></a>Requisitos de memoria y procesador  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] necesitará más recursos de memoria y procesador en los siguientes casos:  
  
-   Cuando se procesen cubos complejos o de gran tamaño. Serán necesarios más recursos de memoria y procesador que en el caso de cubos simples o de pequeño tamaño.  
  
-   Cuando aumente el número de cubos de una misma base de datos.  
  
-   Cuando aumente el número de bases de datos de una misma instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
-   Cuando aumente el número de instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de un mismo equipo.  
  
-   Cuando aumente el número de usuarios que obtienen acceso a los recursos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma simultánea.  
  
 La cantidad de memoria y recursos de procesador disponibles para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] depende de la edición de SQL Server, sistema operativo, capacidad de hardware y de si usa procesadores virtuales o físicos. Para obtener más información, vea estos vínculos:  
  
 [Requisitos de hardware y software para instalar SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
 [Límites de la capacidad de cálculo de cada edición de SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
  
 [Características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
 [Especificaciones de capacidad máxima &#40;Analysis Services&#41;](olap-physical/maximum-capacity-specifications-analysis-services.md)  
  
## <a name="disk-space-requirements"></a>Requisitos de espacio en disco  
 Los distintos aspectos de la instalación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y las tareas relacionadas con el procesamiento de objetos exigen distintas cantidades de espacio en disco. Estos requisitos se describen en la siguiente lista.  
  
 Cubos  
 Los cubos con tablas de hechos de gran tamaño requieren más espacio en disco que los cubos con tablas de hechos de pequeño tamaño. Del mismo modo, aunque en menor medida, los cubos con muchas dimensiones de gran tamaño requieren más espacio en disco que los cubos con menos miembros de dimensión. En general, una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] requerirá aproximadamente un 20 por ciento de la cantidad de espacio necesaria para los mismos datos almacenados en la base de datos relacional subyacente.  
  
 Agregaciones  
 Las agregaciones exigen un espacio adicional proporcional a las agregaciones agregadas; cuantas más agregaciones haya, más espacio será necesario. Si evita la creación de agregaciones innecesarias, lo normal es que el espacio en disco adicional necesario para las agregaciones no supere el 10 por ciento aproximadamente del tamaño de los datos almacenados en la base de datos relacional subyacente.  
  
 Minería de datos  
 De forma predeterminada, las estructuras de minería de datos almacenan en la caché del disco el conjunto de datos con el que se entrenan. Para eliminar estos datos almacenados en la caché del disco, puede utilizar la opción de procesamiento **Procesar borrado de estructura** en el objeto de estructura de minería de datos. Para más información, vea [Requisitos y consideraciones de procesamiento &#40;minería de datos&#41;](../data-mining/processing-requirements-and-considerations-data-mining.md).  
  
 Procesamiento de objetos  
 Durante el procesamiento, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] almacena en disco copias de los objetos que está procesando en la transacción en procesamiento hasta que finaliza el procesamiento. Cuando finaliza el procesamiento, las copias procesadas de los objetos reemplazan a los objetos originales. Por lo tanto, deberá proporcionar suficiente espacio adicional en disco para una segunda copia de cada uno de los objetos que vayan a procesarse. Por ejemplo, si tiene previsto procesar todo un cubo en una única transacción, necesitará suficiente espacio en el disco duro como para almacenar una segunda copia de todo el cubo.  
  
##  <a name="BKMK_Availability"></a> Consideraciones sobre disponibilidad  
 En un entorno de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , es posible que un cubo o un modelo de minería de datos no esté disponible para su consulta debido a un error de hardware o software. También puede ser que un cubo no esté disponible porque necesite procesarse.  
  
### <a name="providing-availability-in-the-event-of-hardware-or-software-failures"></a>Proporcionar disponibilidad en caso de errores de hardware o software  
 Pueden producirse errores de hardware o software por distintas razones. Sin embargo, mantener la disponibilidad de la instalación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no solo es cuestión de solucionar los problemas que originan dichos errores, sino también de proporcionar recursos alternativos que permitan al usuario seguir utilizando el sistema si se produce un error. Normalmente, se utilizan servidores de equilibrio de carga y agrupación en clústeres para proporcionar los recursos alternativos necesarios para mantener la disponibilidad cuando se producen errores de hardware o software.  
  
 Para proporcionar disponibilidad en caso de que se produzca un error de hardware o software, considere la posibilidad de implementar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en un clúster de conmutación por error. En un clúster de conmutación por error, si se produce un error en el nodo principal por cualquier motivo o si éste tiene que reiniciarse, la agrupación en clústeres de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows realiza una conmutación por error al nodo secundario. Tras la conmutación por error, que se produce con gran rapidez, cuando los usuarios ejecuten consultas estarán obteniendo acceso a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se esté ejecutando en el nodo secundario. Para obtener más información sobre los clústeres de conmutación por error, vea [Tecnologías de Windows Server: clústeres de conmutación por error](http://technet.microsoft.com/library/cc732488\(v=WS.10\).aspx).  
  
 Otra solución a los problemas de accesibilidad es implementar el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en dos o varios servidores de producción. Después se puede utilizar la característica de equilibrio de la carga en la red (NLB) de los servidores Windows para combinar los servidores de producción en un único clúster. En un clúster NLB, si alguno de los servidores del clúster no está disponible debido a problemas de hardware o software, el servicio NLB dirige las consultas del usuario a los servidores que siguen estando disponibles.  
  
### <a name="providing-availability-while-processing-structural-changes"></a>Proporcionar disponibilidad durante el procesamiento de cambios estructurales  
 Algunos de los cambios que se realizan en un cubo pueden hacer que el cubo deje de estar disponible hasta que finalice su procesamiento. Por ejemplo, si se realizan cambios estructurales en una de las dimensiones de un cubo, aunque vuelva a procesarse la dimensión, los cubos que utilicen la dimensión modificada también tendrán que procesarse. Hasta que no se hayan procesado dichos cubos, los usuarios no podrán consultarlos ni podrán consultar ningún modelo de minería de datos que se base en un cubo con la dimensión modificada.  
  
 Para proporcionar disponibilidad durante el procesamiento de cambios estructurales que afecten a uno o a varios cubos de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , considere la posibilidad de incorporar un servidor de ensayo y de utilizar el Asistente para sincronizar bases de datos. Esta característica le permitirá actualizar datos y metadatos en un servidor de ensayo y, después, realizar una sincronización en línea del servidor de producción y el servidor de ensayo. Para más información, consulte [Synchronize Analysis Services Databases](synchronize-analysis-services-databases.md).  
  
 Para procesar actualizaciones incrementales de datos de origen de un modo transparente, habilite el almacenamiento en caché automático. El almacenamiento en caché automático actualiza los cubos con nuevos datos de origen sin necesidad de un procesamiento manual y sin que esto afecte a la disponibilidad de los cubos. Para más información, vea [Almacenamiento en caché automático &#40;Particiones&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
##  <a name="BKMK_Scalability"></a> Consideraciones sobre escalabilidad  
 Si hay varias instancias de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en un mismo equipo, pueden producirse problemas de rendimiento. Una opción para resolver estos problemas es aumentar los recursos de procesador, memoria y disco del servidor. No obstante, es posible que también necesite escalar las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] entre varios equipos.  
  
### <a name="scaling-analysis-services-across-multiple-computers"></a>Escalar Analysis Services entre varios equipos  
 Existen varias formas de escalar una instalación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] entre varios equipos. Estas opciones se describen en la siguiente lista.  
  
-   Si hay varias instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en un único equipo, puede mover una o varias instancias a otro equipo.  
  
-   Si hay varias bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en un único equipo, puede mover una o varias de las bases de datos a su propia instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en otro equipo.  
  
-   Si una o varias bases de datos relacionales proporcionan datos a una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , puede mover estas bases de datos a un equipo distinto. Antes de mover las bases de datos, tenga en cuenta la velocidad de la red y el ancho de banda entre la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y sus bases de datos subyacentes. Si la red es lenta o está congestionada, el desplazamiento de las bases de datos subyacentes a otro equipo disminuirá el rendimiento del procesamiento.  
  
-   Si el procesamiento afecta al rendimiento de las consultas, pero no puede llevarlo a cabo en momentos en que la carga de consultas es más reducida, considere la posibilidad de mover las tareas de procesamiento a un servidor de ensayo y, después, realizar una sincronización en línea del servidor de producción y el servidor de ensayo. Para más información, consulte [Synchronize Analysis Services Databases](synchronize-analysis-services-databases.md). También puede distribuir el procesamiento entre varias instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante el uso de particiones remotas. El procesamiento de particiones remotas utiliza los recursos de procesador y memoria del servidor remoto, en lugar de utilizar los recursos del equipo local. Para más información sobre la administración de particiones remotas, vea [Crear y administrar una partición remota &#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md).  
  
-   Si el rendimiento de las consultas es pobre pero no puede aumentar los recursos de procesador y memoria del servidor local, considere la posibilidad de implementar un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en dos o varios servidores de producción. Puede utilizar la funcionalidad de equilibrio de la carga en la red (NLB) para combinar los servidores en un único clúster. En un clúster NLB, las consultas se distribuyen automáticamente entre todos los servidores del clúster NLB.  
  
  
