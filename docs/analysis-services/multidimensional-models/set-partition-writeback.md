---
title: Establecer la reescritura de particiones | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], writeback
- partitions [Analysis Services], write-enabled
- writeback [Analysis Services], partitions
ms.assetid: 38bb09cc-2652-4971-8373-0cf468cdc7a6
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 45057f5e164c473b588df70f5b8a8617f74390d2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-partition-writeback"></a>Establecer la reescritura de particiones
  Si habilita para escritura un grupo de medida, los usuarios finales pueden cambiar los datos del cubo mientras lo examinan; en ese caso, los cambios se guardan en una tabla diferente denominada tabla de reescritura, no en los datos del cubo ni en los datos de origen. Los usuarios finales que examinan una partición habilitada para escritura verán el efecto neto de todos los cambios en la tabla de reescritura de la partición.  
  
 Los datos de reescritura se pueden examinar o eliminar. También puede convertir los datos de reescritura en una partición. En una partición habilitada para escritura, puede utilizar los roles de cubo para conceder acceso de lectura/escritura a usuarios y grupos de usuarios y para limitar el acceso a determinadas celdas o grupos de celdas de la partición.  
  
 Para ver un vídeo corto en el que se ofrece una introducción a la reescritura, vea [Excel 2010 Writeback to Analysis Services](http://go.microsoft.com/fwlink/p/?LinkId=394951). Hay una explicación más detallada de esta característica en esta serie de entradas de blog: [Building a Writeback Application with Analysis Services (Compilar una aplicación de reescritura con Analysis Services) (blog)](http://go.microsoft.com/fwlink/?LinkId=394977).  
  
> [!NOTE]  
>  La reescritura solo se admite para bases de datos relacionales y data marts de SQL Server, y solo para modelos multidimensionales de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="how-to-write-enable-a-partition"></a>Cómo habilitar una partición para escritura  
 Puede habilitar para escritura los grupos de medida de una partición si habilita para escritura la propia partición en el Diseñador de cubos en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   En el Diseñador de cubos, en la pestaña Particiones, haga clic con el botón derecho en una partición y seleccione **Configuración de reescritura**.  
  
-   En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], expanda la base de datos, el cubo y el grupo de medida y, luego, haga clic con el botón derecho en **Reescritura** y seleccione **Habilitar reescritura**.  
  
 La reescritura solo se admite para las medidas que usan la agregación SUM. En la base de datos de ejemplo AdventureWorks, puede utilizar el grupo de medida Destinos de venta para probar los comportamientos de reescritura.  
  
 Cuando se habilita para escritura una partición, se especifica un nombre de tabla y un origen de datos para almacenar la tabla de reescritura. Cualquier cambio posterior en el grupo de medida se almacenará en esta tabla.  
  
## <a name="browse-writeback-data-in-a-partition"></a>Examinar los datos de reescritura en una partición  
 Puede examinar el contenido de la tabla de reescritura de un cubo con el cuadro de diálogo **Examinar datos** , al que puede acceder si hace clic con el botón derecho en una partición habilitada para escritura en la pestaña **Particiones** del Diseñador de cubos.  
  
## <a name="delete-writeback-data-or-disable-writeback"></a>Eliminar datos de reescritura o deshabilitar la reescritura  
 La eliminación de los datos de reescritura elimina la caché de reescritura; cuando esos datos se eliminan, el trabajo adicional de reescritura se lleva a cabo en una pizarra limpia. Deshabilitar la reescritura en una partición de cubo simplemente desactiva la reescritura para esa partición.  
  
## <a name="convert-writeback-data-to-a-partition"></a>Convertir datos de reescritura en una partición  
 Puede convertir los datos de la tabla de reescritura de una partición en una partición. Este procedimiento convierte la tabla de reescritura en la nueva tabla de hechos de la partición.  
  
> [!CAUTION]  
>  El uso incorrecto de las particiones puede provocar que haya datos incorrectos en el cubo. Para más información, vea [Crear y administrar una partición local &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md).  
  
 Al convertir la tabla de datos de reescritura en una partición también se deshabilita la partición para escritura. Todas las directivas de lectura/escritura y permisos de lectura/escritura no restringidos de las celdas de la partición se deshabilitan, y los usuarios finales no podrán cambiar los datos mostrados del cubo. (Los usuarios finales con directivas de lectura/escritura no restringidas deshabilitadas o con permisos de lectura y lectura deshabilitados, seguirán siendo capaces de examinar el cubo.) Los permisos de lectura y de contingente de lectura no se ven afectados.  
  
 Para convertir los datos de reescritura en una partición, use el cuadro de diálogo **Convertir en partición**, al que puede acceder si hace clic con el botón derecho en la tabla de reescritura de una partición habilitada para escritura en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Especifique un nombre para la partición y si va a diseñar la agregación de la partición más adelante o al mismo tiempo que la crea. Para crear la agregación al mismo tiempo que elige la partición, debe elegir copiar el diseño de agregaciones desde una partición existente. Aunque no siempre, ésta suele ser la partición de reescritura actual. También puede elegir procesar la partición al mismo tiempo que la crea.  
  
## <a name="see-also"></a>Vea también  
 [Particiones habilitadas para escritura](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [Habilitar reescritura en un cubo OLAP en el nivel de celda en Excel 2010](http://go.microsoft.com/fwlink/p/?LinkId=394952)   
 [Habilitación y seguridad de entrada de datos con reescritura de Analysis Services](http://go.microsoft.com/fwlink/p/?LinkId=394953)  
  
  
