---
title: Especifique la información de origen (Asistente para particiones) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.partitionwizard.specifydsvandfacttables.f1
ms.assetid: b6c13587-c690-45d9-af90-b3d652afc55b
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1d29067eabeb7050ec033cc5d274f9f5373c97ed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204024"
---
# <a name="specify-source-information-partition-wizard"></a>Especificar información de origen (Asistente para particiones)
  Use la página **Especificar información de origen** para seleccionar el grupo de medida en el que desea crear la partición, así como la vista del origen de datos y las tablas de filtros de la partición.  
  
> [!CAUTION]  
>  Si especifica una tabla en **Tablas disponibles** usada por otra partición, deberá proporcionar una consulta en la página **Restringir filas** para evitar duplicar datos en el cubo.  
  
## <a name="options"></a>Opciones  
 **grupo de medida**  
 Seleccione un grupo de medida para la partición.  
  
 **Look in**  
 Seleccione el origen de datos o la vista del origen de datos que contiene las tablas de origen para la partición. La vista del origen de datos utilizada por el grupo de medida aparece seleccionada de forma predeterminada.  
  
 **Tablas de filtros**  
 Escriba la cadena que quiere usar para restringir las tablas mostradas en **Tablas disponibles**con el nombre de la tabla.  
  
 **Buscar tablas**  
 Seleccione esta opción para actualizar la lista de tablas de **Tablas disponibles**y restringir la lista si se ha especificado una cadena en **Tablas de filtros**.  
  
 **Tablas disponibles**  
 Seleccione las tablas que desea utilizar como tablas de origen para las particiones. El **Asistente para particiones** crea una partición para cada una de las tablas seleccionadas en **Tablas disponibles**.  
  
 Si no ha especificado ningún filtro en **Tablas de filtros**, esta opción mostrará la lista de todas las tablas en el origen de datos o en la vista del origen de datos especificados en **Buscar en** que presenten una estructura similar a la tabla de hechos utilizada por el grupo de medida especificado en **Grupo de medida**.  
  
 Si ha especificado un filtro en **Tablas de filtros**, podrá restringir aún más la lista mediante la comparación del filtro con los nombres de tabla que cumplen los criterios anteriores. Solo se mostrarán las tablas que contengan la cadena especificada en **Tablas de filtros** .  
  
> [!NOTE]  
>  Si selecciona más de una tabla, no podrá mostrarse la página **Restringir filas** y no podrán restringirse las filas para las particiones creadas a partir de las tablas seleccionadas. Para restringir filas en las particiones, ejecute el Asistente para particiones para cada tabla en la que desea crear una partición.  
  
## <a name="see-also"></a>Vea también  
 [Las particiones &#40;Analysis Services - datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  