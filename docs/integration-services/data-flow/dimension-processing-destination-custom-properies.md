---
title: Propiedades personalizadas del destino de procesamiento de dimensiones | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2f46acb401bf04e9b0445c452e26d69de42a2d94
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71292825"
---
# <a name="dimension-processing-destination-custom-properies"></a>Propiedades personalizadas del destino de procesamiento de dimensiones

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El destino Procesamiento de dimensiones tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino Procesamiento de dimensiones. Todas las propiedades son de lectura y escritura.  
  
|Propiedad|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|Cadena de conexión a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|KeyDuplicate|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, valor que indica cómo controlar los errores de clave duplicada. Los valores posibles son **IgnoreError** (0), **ReportAndContinue** (1) y **ReportAndStop** (2). El valor predeterminado de esta propiedad es **IgnoreError** (0).|  
|KeyErrorAction|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, valor que indica cómo controlar los errores de clave. Los valores posibles son **ConvertToUnknown** (0) y **DiscardRecord** (1). El valor predeterminado de esta propiedad es **ConvertToUnknown** (0).|  
|KeyErrorLimit|Entero|Cuando UseDefaultConfiguration es **False**, límite superior de errores de clave que se habilitan.|  
|KeyErrorLimitAction|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, valor que indica la acción que se va a realizar cuando **KeyErrorLimit** se alcanza. Los valores posibles son **StopLogging** (1) y **StopProcessing** (0). El valor predeterminado de esta propiedad es **StopProcessing** (0).|  
|KeyErrorLogFile|String|Cuando UseDefaultConfiguration es **False**, ruta de acceso y el nombre de archivo del archivo de registro de errores.|  
|KeyNotFound|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, valor que indica cómo controlar los errores de la clave que falta. Los valores posibles son **IgnoreError** (0), **ReportAndContinue** (1) y **ReportAndStop** (2). El valor predeterminado de esta propiedad es **IgnoreError** (0).|  
|NullKeyConvertedToUnknown|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, valor que indica cómo controlar las claves NULL que se han convertido en el valor Unknown. Los valores posibles son **IgnoreError** (0), **ReportAndContinue** (1) y **ReportAndStop** (2). El valor predeterminado de esta propiedad es **IgnoreError** (0).|  
|NullKeyNotAllowed|Integer (enumeración)|Cuando UseDefaultConfiguration es **False**, valor que indica cómo controlar los valores NULL no permitidos. Los valores posibles son **IgnoreError** (0), **ReportAndContinue** (1) y **ReportAndStop** (2). El valor predeterminado de esta propiedad es **IgnoreError** (0).|  
|ProcessType|Integer (enumeración)|Tipo de procesamiento de dimensiones utilizado por la transformación. Los valores son **ProcessAdd** (1) (incremental), **ProcessFull** (0) y **ProcessUpdate** (2).|  
|UseDefaultConfiguration|Boolean|Valor que especifica si la transformación usa la configuración de errores predeterminada. Si esta propiedad es **False**, la transformación incluye información sobre el procesamiento de los errores.|  
  
 La entrada y las columnas de entrada de destino de procesamiento de dimensiones no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Dimension Processing Destination](../../integration-services/data-flow/dimension-processing-destination.md).  
  
## <a name="see-also"></a>Consulte también  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
