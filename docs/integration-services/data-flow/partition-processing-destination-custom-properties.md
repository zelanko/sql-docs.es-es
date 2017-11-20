---
title: Propiedades personalizadas del destino de procesamiento de particiones | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9d3ae46aa1d06fd7d4d5a977d40e3b40a5af4170
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="partition-processing-destination-custom-properties"></a>Propiedades personalizadas del destino de procesamiento de particiones
  El destino Procesamiento de particiones tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino Procesamiento de particiones. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Description|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|Cadena de conexión a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|KeyDuplicate|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, valor que indica cómo controlar los errores de clave duplicada. Los valores posibles son **IgnoreError** (0), **ReportAndContinue** (1) y **ReportAndStop** (2). El valor predeterminado de esta propiedad es **IgnoreError** (0).|  
|KeyErrorAction|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, un valor que indica cómo controlar los errores de clave. Los valores posibles son **ConvertToUnknown** (0) y **DiscardRecord** (1). El valor predeterminado de esta propiedad es **ConvertToUnknown** (0).|  
|KeyErrorLimit|Integer|Cuando UseDefaultConfiguration es **False**, el límite superior de errores de clave que se permiten.|  
|KeyErrorLimitAction|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, valor que indica la acción que se va a realizar cuando **KeyErrorLimit** se alcanza. Los valores posibles son **StopLogging** (1) y **StopProcessing** (0). El valor predeterminado de esta propiedad es **StopProcessing** (0).|  
|KeyErrorLogFile|String|Cuando UseDefaultConfiguration es **False**, ruta de acceso y el nombre de archivo del archivo de registro de errores.|  
|KeyNotFound|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, valor que indica cómo controlar los errores de la clave que falta. Los valores posibles son **IgnoreError** (0), **ReportAndContinue** (1) y **ReportAndStop** (2). El valor predeterminado de esta propiedad es **ReportAndContinue** (1).|  
|NullKeyConvertedToUnknown|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, un valor que indica cómo controlar las claves NULL que se han convertido en el valor Unknown. Los valores posibles son **IgnoreError** (0), **ReportAndContinue** (1) y **ReportAndStop** (2). El valor predeterminado de esta propiedad es **IgnoreError** (0).|  
|NullKeyNotAllowed|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, valor que indica cómo controlar los valores NULL no permitidos. Los valores posibles son **IgnoreError** (0), **ReportAndContinue** (1) y **ReportAndStop** (2). El valor predeterminado de esta propiedad es **ReportAndContinue** (1).|  
|ProcessType|Integer (enumeración)|Tipo de procesamiento de particiones utilizado por la transformación. Los valores posibles son **ProcessAdd** (1) (incremental), **ProcessFull** (0) y **ProcessUpdate** (2).|  
|UseDefaultConfiguration|Boolean|Valor que especifica si la transformación usa la configuración de errores predeterminada. Si esta propiedad es **False**, la transformación usa los valores de propiedades personalizadas de control de errores que se enumeran en esta tabla, incluidos KeyDuplicate y KeyErrorAction entre otros.|  
  
 La entrada y las columnas de entrada de destino de procesamiento de particiones no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Partition Processing Destination](../../integration-services/data-flow/partition-processing-destination.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  

