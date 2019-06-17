---
title: Propiedades personalizadas del destino de procesamiento de dimensiones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b63e508f87b9766507c541a7ed81e42466bbd1e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62827364"
---
# <a name="dimension-processing-destination-custom-properies"></a>Propiedades personalizadas del destino de procesamiento de dimensiones
  El destino Procesamiento de dimensiones tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino Procesamiento de dimensiones. Todas las propiedades son de lectura y escritura.  
  
|Property|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|Cadena de conexión a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|KeyDuplicate|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, un valor que indica cómo controlar errores de clave duplicada. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1) y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `IgnoreError` (0).|  
|KeyErrorAction|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, un valor que indica cómo controlar errores de clave. Los valores posibles son `ConvertToUnknown` (0) y `DiscardRecord` (1). El valor predeterminado de esta propiedad es `ConvertToUnknown` (0).|  
|KeyErrorLimit|Integer|Cuando UseDefaultConfiguration es `False`, el límite de errores de clave que están habilitadas.|  
|KeyErrorLimitAction|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, un valor que indica la acción que se va a realizar cuando `KeyErrorLimit` se alcanza. Los valores posibles son `StopLogging` (1) y `StopProcessing` (0). El valor predeterminado de esta propiedad es `StopProcessing` (0).|  
|KeyErrorLogFile|String|Cuando UseDefaultConfiguration es `False`, la ruta de acceso y el nombre del archivo de registro de errores.|  
|KeyNotFound|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, un valor que indica cómo controlar errores de clave que falta. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1) y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `IgnoreError` (0).|  
|NullKeyConvertedToUnknown|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, convertir un valor que indica cómo controlar las claves null en el valor unknown. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1) y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `IgnoreError` (0).|  
|NullKeyNotAllowed|Integer (enumeración)|Cuando UseDefaultConfiguration es `False`, un valor que indica cómo controlar valores NULL no permitidos. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1) y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `IgnoreError` (0).|  
|ProcessType|Integer (enumeración)|Tipo de procesamiento de dimensiones utilizado por la transformación. Los valores son `ProcessAdd` (1) (incremental), `ProcessFull` (0), y `ProcessUpdate` (2).|  
|UseDefaultConfiguration|Boolean|Valor que especifica si la transformación usa la configuración de errores predeterminada. Si esta propiedad es `False`, la transformación incluye información sobre el procesamiento de los errores.|  
  
 La entrada y las columnas de entrada de destino de procesamiento de dimensiones no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Dimension Processing Destination](dimension-processing-destination.md).  
  
## <a name="see-also"></a>Vea también  
 [Common Properties](../common-properties.md)  
  
  
