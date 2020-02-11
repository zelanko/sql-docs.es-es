---
title: Editor de destino de procesamiento de particiones (página avanzadas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partprocessingtransformation.advanced.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 2039ee0f-069d-479d-90b2-2a12481b1162
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: de7c84a463d15e3260cc64c53ba1f82c6808dd93
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056776"
---
# <a name="partition-processing-destination-editor-advanced-page"></a>Editor de destino de procesamiento de particiones (página Avanzadas)
  Utilice la página **Avanzadas** del cuadro de diálogo **Editor de destino de procesamiento de particiones** para configurar el control de errores.  
  
 Para obtener más información acerca del destino de procesamiento de particiones, vea [Partition Processing Destination](data-flow/partition-processing-destination.md).  
  
> [!NOTE]  
>  Las tareas aquí descritas no se aplican a los modelos tabulares de Analysis Services.  No se pueden asignar las columnas de entrada a las de partición para los modelos tabulares. En su lugar puede usar la tarea Ejecutar DDL de Analysis Services [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) para procesar la partición.  
  
## <a name="options"></a>Opciones  
 **Usar la configuración de error predeterminada.**  
 Especifica si debe utilizarse el control de errores predeterminado de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . De manera predeterminada, este valor es `True`.  
  
 **Acción de error de clave**  
 Permite especificar la forma de controlar registros que tienen valores de clave no aceptables.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**ConvertToUnknown**|Convierte el valor de clave no aceptable en el valor Unknown.|  
|**DiscardRecord**|Descarta el registro.|  
  
 **Omitir errores**  
 Especifica que deben omitirse los errores.  
  
 **Detener tras error**  
 Especifica que el procesamiento debe detenerse cuando se produce un error.  
  
 **Número de errores**  
 Especifica el umbral de error donde debe detenerse el procesamiento, en caso de que se haya seleccionado **Detenerse ante errores**.  
  
 **Acción en el error**  
 Especifica la acción que debe llevarse a cabo cuando se alcanza el umbral de error, en caso de que se haya seleccionado **Detenerse ante errores**.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**StopProcessing**|Detiene el procesamiento.|  
|**StopLogging**|Detiene el registro de errores.|  
  
 **No se encontró la clave**  
 Especifica la acción que debe llevarse a cabo en caso de que se produzca un error de clave no encontrada. Este valor es **ReportAndContinue**de forma predeterminada.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**IgnoreError**|Omite el error y reanuda el procesamiento.|  
|**ReportAndContinue**|Informa del error y reanuda el procesamiento.|  
|**ReportAndStop**|Informa del error y detiene el procesamiento.|  
  
 **Clave duplicada**  
 Especifica la acción que debe llevarse a cabo en caso de que se produzca un error de clave duplicada. Este valor es **IgnoreError**de forma predeterminada.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**IgnoreError**|Omite el error y reanuda el procesamiento.|  
|**ReportAndContinue**|Informa del error y reanuda el procesamiento.|  
|**ReportAndStop**|Informa del error y detiene el procesamiento.|  
  
 **Clave null convertida en Unknown**  
 Especifica la acción que debe llevarse a cabo cuando una clave NULL se ha convertido al valor Unknown. Este valor es **IgnoreError**de forma predeterminada.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**IgnoreError**|Omite el error y reanuda el procesamiento.|  
|**ReportAndContinue**|Informa del error y reanuda el procesamiento.|  
|**ReportAndStop**|Informa del error y detiene el procesamiento.|  
  
 **Clave null no permitida**  
 Especifica la acción que debe llevarse a cabo cuando no se permiten claves NULL y se encuentra una clave NULL. Este valor es **ReportAndContinue**de forma predeterminada.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**IgnoreError**|Omite el error y reanuda el procesamiento.|  
|**ReportAndContinue**|Informa del error y reanuda el procesamiento.|  
|**ReportAndStop**|Informa del error y detiene el procesamiento.|  
  
 **Ruta de acceso del registro de errores**  
 Escriba la ruta de acceso al registro de errores o seleccione un destino mediante el botón para examinar **(…)** .  
  
 **Examinar (...)**  
 Seleccione una ruta de acceso para el registro de errores.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [&#40;página asignaciones del editor de destino de procesamiento de particiones&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)  
  
  
