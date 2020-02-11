---
title: Propiedades personalizadas del destino de procesamiento de particiones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3dbab24f756498d7427f9961e4176249daac8dfb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62770951"
---
# <a name="partition-processing-destination-custom-properties"></a>Propiedades personalizadas del destino de procesamiento de particiones
  El destino Procesamiento de particiones tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino Procesamiento de particiones. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|Cadena de conexión a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|KeyDuplicate|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, valor que indica cómo controlar los errores de clave duplicada. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1) y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `IgnoreError` (0).|  
|KeyErrorAction|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, valor que indica cómo controlar los errores de clave. Los valores posibles son `ConvertToUnknown` (0) y `DiscardRecord` (1). El valor predeterminado de esta propiedad es `ConvertToUnknown` (0).|  
|KeyErrorLimit|Entero|Cuando UseDefaultConfiguration es `False`, se permite el límite superior de errores de clave.|  
|KeyErrorLimitAction|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, valor que indica la acción que se realizará `KeyErrorLimit` cuando se alcance. Los valores posibles son `StopLogging` (1) y `StopProcessing` (0). El valor predeterminado de esta propiedad es `StopProcessing` (0).|  
|KeyErrorLogFile|String|Cuando UseDefaultConfiguration es `False`, la ruta de acceso y el nombre de archivo del archivo de registro de errores.|  
|KeyNotFound|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, valor que indica cómo controlar los errores de clave que faltan. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1) y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `ReportAndContinue` (1).|  
|NullKeyConvertedToUnknown|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, valor que indica cómo controlar las claves null convertidas en el valor desconocido. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1) y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `IgnoreError` (0).|  
|NullKeyNotAllowed|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, valor que indica cómo controlar los valores NULL no permitidos. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1) y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `ReportAndContinue` (1).|  
|ProcessType|Integer (enumeración)|Tipo de procesamiento de particiones utilizado por la transformación. Los valores posibles son `ProcessAdd` (1) (incremental), `ProcessFull` (0) y `ProcessUpdate` (2).|  
|UseDefaultConfiguration|Boolean|Valor que especifica si la transformación usa la configuración de errores predeterminada. Si esta propiedad es `False`, la transformación utiliza los valores de las propiedades personalizadas de control de errores que se muestran en esta tabla, como KeyDuplicate, KeyErrorAction, etc.|  
  
 La entrada y las columnas de entrada de destino de procesamiento de particiones no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Partition Processing Destination](partition-processing-destination.md).  
  
## <a name="see-also"></a>Consulte también  
 [Common Properties](../common-properties.md)  
  
  
