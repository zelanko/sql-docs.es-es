---
title: Editor de destino de procesamiento de dimensiones (página avanzadas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 2b30835a-2680-4d98-89a4-4f17e29e3818
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 07a04fe26bbd47463d0564f7799698ab282a9979
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66059485"
---
# <a name="dimension-processing-destination-editor-advanced-page"></a>Editor de destino de procesamiento de dimensiones (página Avanzadas)
  Utilice la página **Avanzadas** del cuadro de diálogo **Editor de destino de procesamiento de dimensiones** para configurar el control de errores.  
  
 Para obtener más información acerca del destino de procesamiento de dimensiones, vea [Dimension Processing Destination](data-flow/dimension-processing-destination.md).  
  
## <a name="options"></a>Opciones  
 **Usar la configuración de error predeterminada.**  
 Especifica si debe utilizarse el control de errores predeterminado de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . De manera predeterminada, este valor es `True`.  
  
 **Acción de error de clave**  
 Permite especificar la forma de controlar registros que tienen valores de clave no aceptables.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**ConvertToUnknown**|Convierte el valor de clave no aceptable en el valor `UnknownMember`.|  
|**DiscardRecord**|Descarta el registro.|  
  
 **Omitir errores**  
 Especifica que deben omitirse los errores.  
  
 **Detener tras error**  
 Especifica que el procesamiento debe detenerse cuando se produce un error.  
  
 **Número de errores**  
 Especifica el umbral de error donde tiene que detenerse el procesamiento (si ha seleccionado **Detenerse ante errores**).  
  
 **Acción en el error**  
 Especifica la acción que se realizará cuando se alcance el umbral de error (si ha seleccionado **Detenerse ante errores**).  
  
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
 Especifica la acción que debe llevarse a cabo cuando una clave NULL se ha convertido en el valor `UnknownMember`. Este valor es **IgnoreError**de forma predeterminada.  
  
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
 Escriba la ruta de acceso al registro de errores, o bien haga clic en el botón **Examinar (…)** para seleccionar un destino.  
  
 **Examinar (...)**  
 Seleccione una ruta de acceso para el registro de errores.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de procesamiento de dimensiones &#40;página Administrador de conexiones&#41;](../../2014/integration-services/dimension-processing-destination-editor-connection-manager-page.md)   
 [Editor de destino de procesamiento de dimensiones &#40;página asignaciones&#41;](../../2014/integration-services/dimension-processing-destination-editor-mappings-page.md)  
  
  
