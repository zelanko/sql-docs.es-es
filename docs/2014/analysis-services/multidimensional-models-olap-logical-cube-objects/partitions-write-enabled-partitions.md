---
title: Particiones habilitadas para escritura | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], write-enabled
- partitions [Analysis Services], storage
- writeback [Analysis Services], partitions
- storing data [Analysis Services], partitions
ms.assetid: 46e7683f-03ce-4af2-bd99-a5203733d723
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8429c02d84520524906fb0fbd411ee0a49169815
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194645"
---
# <a name="write-enabled-partitions"></a>Particiones habilitadas para escritura
  Los datos de un cubo son normalmente de solo lectura. Con todo, en ciertos casos, puede interesarle habilitar una partición para escritura. Las particiones habilitadas para escritura se usan para que los usuarios corporativos puedan explorar escenarios si cambian los valores de las celdas y analizan los efectos de los cambios en los datos del cubo. Si habilita una partición para escritura, las aplicaciones cliente podrán registrar los cambios en los datos de la partición. Estos cambios, conocidos como datos de reescritura, se almacenan en una tabla independiente y no sobrescriben los datos existentes en un grupo de medida. Sin embargo, se incorporan a los resultados de la consulta como si formasen parte de los datos del cubo.  
  
 Puede habilitar para escritura un cubo completo o solo algunas particiones del mismo. Las dimensiones habilitadas para escritura son distintas, aunque complementarias. Una partición habilitada para escritura permite a los usuarios actualizar celdas de particiones, mientras que las dimensiones habilitadas para escritura les permiten actualizar miembros de dimensión. También se pueden utilizar conjuntamente estas dos características. Por ejemplo, un cubo habilitado para escritura o una partición habilitada para escritura no tiene que incluir ninguna dimensión habilitada para escritura. **Tema relacionado:**[dimensiones habilitadas para escritura](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
> [!NOTE]  
>  Si desea habilitar para escritura un cubo que tiene una base de datos de Microsoft Access como origen de datos, no utilice el proveedor Microsoft OLE DB para controladores ODBC en las definiciones de origen de datos del cubo, sus particiones ni sus dimensiones. En su lugar, puede utilizar el proveedor OLE DB de Microsoft Jet 4.0 o cualquier versión del Jet Service Pack que incluya Jet 4.0 OLE. Para obtener más información, consulte el artículo de Microsoft Knowledge Base [cómo obtener el service pack más reciente para el motor de base de datos Microsoft Jet 4.0](http://support.microsoft.com/?kbid=239114).  
  
 Un cubo solamente puede habilitarse para escritura si todas sus medidas utilizan la función de agregado `Sum`. Los grupos de medida vinculados y los cubos locales no pueden habilitarse para escritura.  
  
## <a name="writeback-storage"></a>Almacenamiento de reescritura  
 Cualquier cambio realizado por un usuario corporativo se almacena en una tabla de reescritura como una diferencia en relación con el valor que se muestra actualmente. Por ejemplo, si un usuario final cambia el valor de una celda de 90 a 100, en la tabla de reescritura se almacena el valor `+10`, junto con la hora del cambio e información sobre el usuario corporativo que lo llevó a cabo. En las aplicaciones cliente se muestra el efecto neto de los cambios acumulados. Se conserva el valor original del cubo y en la tabla de reescritura se registra un seguimiento de autoría de los cambios.  
  
 Los cambios realizados en celdas hoja y no hoja se controlan de manera diferente. Una celda hoja representa una intersección de una medida y un miembro hoja de cada dimensión a la que hace referencia el grupo de medida. El valor de una celda hoja se toma directamente de la tabla de hechos y no puede dividirse mediante la obtención de detalles. Si un cubo o alguna partición están habilitados para escritura, se pueden realizar cambios en una celda hoja. En una celda no hoja solo pueden realizarse cambios si la aplicación cliente proporciona una forma de distribuir los cambios entre las celdas hoja que forman la celda no hoja. Este proceso, denominado asignación, se administra mediante la instrucción UPDATE CUBE en expresiones multidimensionales (MDX). Los desarrolladores de Business Intelligence pueden utilizar la instrucción UPDATE CUBE para incluir la funcionalidad de asignación. Para obtener más información, consulte [instrucción UPDATE CUBE &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube).  
  
> [!IMPORTANT]  
>  Si las celdas actualizadas no se superponen, se puede utilizar la propiedad de la cadena de conexión `Update Isolation Level` para mejorar el rendimiento de UPDATE CUBE. Para obtener más información, consulta <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.  
  
 Independientemente de que la aplicación cliente distribuya los cambios realizados en las celdas no hoja, siempre que se evalúen consultas, los cambios de la tabla de reescritura se aplican tanto a las celdas hoja como no hoja, de manera que los usuarios corporativos puedan ver los efectos de los cambios en todo el cubo.  
  
 Los cambios realizados por el usuario corporativo se mantienen en una tabla de reescritura independiente con la que se puede trabajar de la manera siguiente:  
  
-   Convertir en una partición para incorporar permanentemente los cambios al cubo. Esta acción hace que el grupo de medida sea de solo lectura. Puede especificar una expresión de filtro para seleccionar los cambios que desea convertir.  
  
-   Descartar los cambios para devolver la partición a su estado original. Esta acción hace que la partición sea de solo lectura.  
  
## <a name="security"></a>Seguridad  
 Los usuarios corporativos solo podrán registrar los cambios en la tabla de reescritura de un cubo si pertenecen a un rol que tiene permiso de lectura y escritura para las celdas del cubo. En cada rol, puede controlar las celdas del cubo que pueden o no actualizarse. Para obtener más información, consulte [conceder permisos para cubos o modelos &#40;Analysis Services&#41;](../multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Dimensiones habilitadas para escritura](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)   
 [Las agregaciones y diseños de agregaciones](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [Las particiones &#40;Analysis Services - datos multidimensionales&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Dimensiones habilitadas para escritura](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
