---
title: (Pestaña particiones, Diseñador de cubos) de grupos de medida (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitionspane.measuregroupdetail.f1
ms.assetid: 58e44b24-cfcd-4908-b445-d4374b961b98
caps.latest.revision: 24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a372e8418692c0db98332b7fa67d8563265d1de4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249445"
---
# <a name="measure-groups-partitions-tab-cube-designer-analysis-services---multidimensional-data"></a>Grupos de medida (pestaña Particiones, Diseñador de cubos) (Analysis Services - Datos multidimensional)
  Use el panel **Grupos de medida** de la pestaña **Particiones** del Diseñador de cubos para administrar las particiones asociadas con cada grupo de medida del cubo.  
  
## <a name="options"></a>Opciones  
 **Particiones**  
 Muestra una cuadrícula que contiene la lista de particiones compatibles con el grupo de medida seleccionado. La cuadrícula contiene las columnas siguientes:  
  
 **(Ordinal)**  
 Muestra la posición ordinal de la partición dentro del grupo de medida.  
  
 Haga clic para seleccionar toda la fila para la partición.  
  
 **Nombre de partición**  
 Escriba el nombre de la partición seleccionada.  
  
 **Source**  
 Escriba el nombre de la tabla (para enlace de tablas) o la consulta (para enlace de consultas) que proporciona los datos de la tabla de hechos para la partición seleccionada.  
  
 Haga clic en el botón **...** para ver el cuadro de diálogo **Origen de la partición** y defina el origen de la partición seleccionada.  
  
 **Agregación**  
 Muestra el modo de agregación y el modo de almacenamiento de la partición. El modo de almacenamiento se muestra primero: el procesamiento analítico en línea relacional (ROLAP), el procesamiento analítico en línea multidimensional (MOLAP) o el procesamiento analítico en línea híbrido (HOLAP). El modo de agregación se muestra como un porcentaje de la optimización solicitada, como una medida del espacio solicitado o utilizado, o como el número de agregaciones creadas. Haga clic en el botón **...** para ver el **Asistente para diseñar agregaciones** y defina el diseño de agregaciones de la partición especificada.  
  
 **Descripción**  
 Escriba la descripción opcional de la partición.  
  
 **Nueva partición...**  
 Haga clic para ver el **Asistente para particiones** y crear una nueva partición en el grupo de medida seleccionado.  
  
 **Configuración de almacenamiento...**  
 Haga clic para ver el cuadro de diálogo **Configuración de almacenamiento** y especifique el modo de almacenamiento, el almacenamiento en caché automático y la configuración de notificación para la partición seleccionada.  
  
> [!NOTE]  
>  Esta opción solo se habilita si se ha seleccionado una celda de partición en la cuadrícula **Particiones** del grupo de medida seleccionado.  
  
 **Configuración de reescritura...**  
 Haga clic para mostrar el cuadro de diálogo **Enable/Disable Writeback** (Habilitar/Deshabilitar reescritura) y especifique la configuración de reescritura para el grupo de medida seleccionado.  
  
## <a name="context-menu"></a>Menú contextual  
 Las siguientes opciones están disponibles en el menú contextual que se muestra al hacer clic con el botón derecho en una fila de la cuadrícula **Particiones** del grupo de medida seleccionado:  
  
|Opción|Definición|  
|------------|----------------|  
|**Agregar Business Intelligence**|Haga clic en esta opción para mostrar el **Asistente de Business Intelligence** y agregar características de Business Intelligence al cubo. Para obtener más información sobre el **Asistente de Business Intelligence**, vea [Asistente de Business Intelligence (Ayuda F1)](business-intelligence-wizard-f1-help.md).|  
|**Nueva partición**|Haga clic para ver el **Asistente para particiones** y crear una nueva partición en el grupo de medida seleccionado.|  
|**Cambiar el nombre de partición**|Seleccione esta opción para cambiar el nombre de la partición seleccionada.|  
|**Eliminar**|Haga clic para mostrar el cuadro de diálogo **Eliminar objetos** y eliminar la acción seleccionada.<br /><br /> Nota: Esta opción está deshabilitada si se ha seleccionado una partición de reescritura.|  
|**Diseñar agregaciones**|Haga clic en esta opción para mostrar el **Asistente para diseñar agregaciones** y crear un diseño de agregaciones para la partición seleccionada.<br /><br /> Nota: Esta opción está deshabilitada si se ha seleccionado una partición de reescritura.|  
|**Configuración de almacenamiento**|Haga clic para ver el cuadro de diálogo **Configuración de almacenamiento** y especifique el modo de almacenamiento, el almacenamiento en caché automático y la configuración de notificación para la partición seleccionada.|  
|**Configuración de reescritura**|Haga clic para mostrar el cuadro de diálogo **Enable/Disable Writeback** (Habilitar/Deshabilitar reescritura) y especifique la configuración de reescritura para el grupo de medida que contiene la partición seleccionada.|  
|**Optimización basada en uso**|Haga clic para mostrar el **Asistente para optimización basada en el uso** y cree un diseño de agregaciones basado en los patrones de uso existentes para la partición seleccionada.<br /><br /> Nota: Esta opción está deshabilitada si se ha seleccionado una partición de reescritura.|  
|**Procesar**|Haga clic para mostrar el cuadro de diálogo **Proceso** y procese la partición seleccionada.|  
|**Copiar**|Esta opción está deshabilitada.|  
|**Pegar**|Esta opción está deshabilitada.|  
|**Propiedades**|Seleccione esta opción para mostrar la ventana **Propiedades** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para la partición seleccionada.|  
  
  
