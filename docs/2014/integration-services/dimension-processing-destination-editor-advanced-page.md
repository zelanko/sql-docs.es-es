---
title: Editor de destino de procesamiento de dimensiones (página avanzadas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 2b30835a-2680-4d98-89a4-4f17e29e3818
caps.latest.revision: 27
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3947568a5fed3c2a2467741e93928380ba472e0a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254657"
---
# <a name="dimension-processing-destination-editor-advanced-page"></a>Editor de destino de procesamiento de dimensiones (página Avanzadas)
  Utilice la página **Avanzadas** del cuadro de diálogo **Editor de destino de procesamiento de dimensiones** para configurar el control de errores.  
  
 Para obtener más información acerca del destino de procesamiento de dimensiones, vea [Dimension Processing Destination](data-flow/dimension-processing-destination.md).  
  
## <a name="options"></a>Opciones  
 **Utilizar la configuración de error predeterminada**  
 Especifica si debe utilizarse el control de errores predeterminado de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Este valor es `True` de forma predeterminada.  
  
 **Acción del error de clave**  
 Permite especificar la forma de controlar registros que tienen valores de clave no aceptables.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**ConvertToUnknown**|Convierte el valor de clave no aceptable en el valor `UnknownMember`.|  
|**DiscardRecord**|Descarta el registro.|  
  
 **Omitir errores**  
 Especifica que deben omitirse los errores.  
  
 **Detenerse ante errores**  
 Especifica que el procesamiento debe detenerse cuando se produce un error.  
  
 **Número de errores**  
 Especifica el umbral de error donde tiene que detenerse el procesamiento (si ha seleccionado **Detenerse ante errores**).  
  
 **Acción ante el error**  
 Especifica la acción que se realizará cuando se alcance el umbral de error (si ha seleccionado **Detenerse ante errores**).  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**StopProcessing**|Detiene el procesamiento.|  
|**StopLogging**|Detiene el registro de errores.|  
  
 **Clave no encontrada**  
 Especifica la acción que debe llevarse a cabo en caso de que se produzca un error de clave no encontrada. Este valor es **ReportAndContinue**de forma predeterminada.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**IgnoreError**|Omite el error y reanuda el procesamiento.|  
|**ReportAndContinue**|Informa del error y reanuda el procesamiento.|  
|**ReportAndStop**|Informa del error y detiene el procesamiento.|  
  
 **Clave duplicada**  
 Especifica la acción que debe llevarse a cabo en caso de que se produzca un error de clave duplicada. Este valor es **IgnoreError**de forma predeterminada.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**IgnoreError**|Omite el error y reanuda el procesamiento.|  
|**ReportAndContinue**|Informa del error y reanuda el procesamiento.|  
|**ReportAndStop**|Informa del error y detiene el procesamiento.|  
  
 **Clave NULL convertida en desconocida**  
 Especifica la acción que debe llevarse a cabo cuando una clave NULL se ha convertido en el valor `UnknownMember`. Este valor es **IgnoreError**de forma predeterminada.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**IgnoreError**|Omite el error y reanuda el procesamiento.|  
|**ReportAndContinue**|Informa del error y reanuda el procesamiento.|  
|**ReportAndStop**|Informa del error y detiene el procesamiento.|  
  
 **Clave NULL no permitida**  
 Especifica la acción que debe llevarse a cabo cuando no se permiten claves NULL y se encuentra una clave NULL. Este valor es **ReportAndContinue**de forma predeterminada.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**IgnoreError**|Omite el error y reanuda el procesamiento.|  
|**ReportAndContinue**|Informa del error y reanuda el procesamiento.|  
|**ReportAndStop**|Informa del error y detiene el procesamiento.|  
  
 **Ruta de acceso del registro de errores**  
 Escriba la ruta de acceso al registro de errores, o bien haga clic en el botón **Examinar (…)** para seleccionar un destino.  
  
 **Examinar (...)**  
 Seleccione una ruta de acceso para el registro de errores.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de procesamiento de dimensiones &#40;página Administrador de conexiones&#41;](../../2014/integration-services/dimension-processing-destination-editor-connection-manager-page.md)   
 [Editor de destino de procesamiento de dimensiones &#40;página asignaciones&#41;](../../2014/integration-services/dimension-processing-destination-editor-mappings-page.md)  
  
  
