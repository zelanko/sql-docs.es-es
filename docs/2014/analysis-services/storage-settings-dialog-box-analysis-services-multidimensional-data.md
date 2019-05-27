---
title: Cuadro de diálogo de configuración de almacenamiento (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.f1
- sql12.asvs.cubeeditor.cubebuilder.measuregroupstoragesettings.f1
ms.assetid: 80c41c71-226c-45fe-b9cf-af824b592fe1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ecd796d2fb2bc37c4c2ad6d9fac00ef4258ec038
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66068030"
---
# <a name="storage-settings-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Configuración de almacenamiento (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Configuración de almacenamiento** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para establecer la configuración del almacenamiento en caché automático, del almacenamiento y de las notificaciones para una dimensión, un cubo, un grupo de medida o una partición. Puede abrir el cuadro de diálogo **Configuración de almacenamiento** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] de distintas maneras:  
  
-   Al hacer clic en el botón de puntos suspensivos (**...** ) para el `ProactiveCaching` valor de propiedad de una dimensión, cubo, grupo de medida o partición en la **propiedades** ventana de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
-   Expandir un grupo de medida en la pestaña **Particiones** del **Diseñador de cubos** y hacer clic en **Configuración de almacenamiento**.  
  
-   Expandir un grupo de medida y seleccionar una partición en la cuadrícula para dicho grupo de medida en la pestaña **Particiones** del **Diseñador de cubos** y, a continuación, hacer clic en **Configuración de almacenamiento**.  
  
-   Expandir un grupo de medida y seleccionar una partición en la cuadrícula para dicho grupo de medida en la pestaña **Particiones** del **Diseñador de cubos** y, a continuación, hacer clic en **Configuración de almacenamiento** en el panel **Barra de herramientas** de la pestaña **Particiones** del **Diseñador de cubos**.  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|Valores|  
|----------|----------------|------------|  
|**Configuración estándar**|Seleccione esta opción para habilitar el control deslizante de la opción **Configuración estándar** y utilice los parámetros de configuración predefinidos para el modo de almacenamiento y las características de almacenamiento en caché automático.||  
|**Configuración estándar**|Establezca una de las siguientes configuraciones predefinidas:<br /><br /> **ROLAP en tiempo real**<br /><br /> Seleccione esta opción para utilizar los siguientes parámetros de configuración de almacenamiento y almacenamiento en caché automático:|Modo de almacenamiento ROLAP<br /><br /> Habilita el almacenamiento en caché automático<br /><br /> Quita la caché no actualizada, con un periodo de latencia de 0 segundos<br /><br /> Pone el objeto en línea de forma inmediata|  
||**HOLAP en tiempo real**<br /><br /> Seleccione esta opción para utilizar los siguientes parámetros de configuración de almacenamiento y almacenamiento en caché automático:|Modo de almacenamiento HOLAP<br /><br /> Habilita el almacenamiento en caché automático<br /><br /> Quita la caché no actualizada, con un periodo de latencia de 0 segundos<br /><br /> Actualiza la caché cuando se producen cambios en los datos, con un intervalo de latencia de 0 segundos y sin reemplazo de intervalo de latencia<br /><br /> Pone el objeto en línea de forma inmediata|  
||**MOLAP de latencia baja**<br /><br /> Seleccione esta opción para utilizar los siguientes parámetros de configuración de almacenamiento y almacenamiento en caché automático:|Modo de almacenamiento MOLAP<br /><br /> Habilita el almacenamiento en caché automático<br /><br /> Quita la caché no actualizada, con un periodo de latencia de 30 minutos<br /><br /> Actualiza la caché cuando se producen cambios en los datos, con un intervalo de latencia de 10 segundos y un reemplazo de intervalo de latencia de 10 minutos<br /><br /> Pone el objeto en línea de forma inmediata|  
||**MOLAP de latencia media**<br /><br /> Seleccione esta opción para utilizar los siguientes parámetros de configuración de almacenamiento y almacenamiento en caché automático:|Modo de almacenamiento MOLAP<br /><br /> Habilita el almacenamiento en caché automático<br /><br /> Quita la caché no actualizada, con un periodo de latencia de 4 horas<br /><br /> Actualiza la caché cuando se producen cambios en los datos, con un intervalo de latencia de 10 segundos y un reemplazo de intervalo de latencia de 10 minutos<br /><br /> Pone el objeto en línea de forma inmediata|  
||**MOLAP automático**<br /><br /> Seleccione esta opción para utilizar los siguientes parámetros de configuración de almacenamiento y almacenamiento en caché automático:|Modo de almacenamiento MOLAP<br /><br /> Habilita el almacenamiento en caché automático<br /><br /> Actualiza la caché cuando se producen cambios en los datos, con un intervalo de latencia de 0 segundos y sin reemplazo de intervalo de latencia|  
||**MOLAP programado**<br /><br /> Seleccione esta opción para utilizar los siguientes parámetros de configuración de almacenamiento y almacenamiento en caché automático:|Modo de almacenamiento MOLAP<br /><br /> Habilita el almacenamiento en caché automático<br /><br /> Actualiza la caché de forma periódica, con un intervalo de regeneración de 1 día|  
||**MOLAP**<br /><br /> Seleccione esta opción para utilizar los siguientes parámetros de configuración de almacenamiento y almacenamiento en caché automático:|Modo de almacenamiento MOLAP|  
|**Configuración personalizada**|Seleccione esta opción para establecer de forma explícita las opciones de modo de almacenamiento, almacenamiento en caché automático y notificación.||  
|**Opciones**|Haga clic para abrir el cuadro de diálogo **Opciones de almacenamiento** para establecer explícitamente las opciones de modo de almacenamiento, almacenamiento en caché automático y notificación. Para más información, sobre el cuadro de diálogo **Opciones de almacenamiento**, vea [Cuadro de diálogo Opciones de almacenamiento &#40;Analysis Services - Datos multidimensionales&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md).||  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Almacenamiento en caché automático &#40;particiones&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 [Almacenamiento de cubos &#40;Analysis Services - datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/cube-storage-analysis-services-multidimensional-data.md)  
  
  
