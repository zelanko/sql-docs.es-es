---
title: Propiedades personalizadas del destino de procesamiento de particiones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2724682cebfcae1e5c6a14b9c7cd815c96ad4a7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112512"
---
# <a name="partition-processing-destination-custom-properties"></a>Propiedades personalizadas del destino de procesamiento de particiones
  El destino Procesamiento de particiones tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino Procesamiento de particiones. Todas las propiedades son de lectura y escritura.  
  
|Property|Tipo de datos|Descripción|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|Cadena de conexión a un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|KeyDuplicate|Integer (enumeración)|Cuando es UseDefaultConfiguration `False`, un valor que indica cómo controlar errores de clave duplicada. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1), y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `IgnoreError` (0).|  
|KeyErrorAction|Integer (enumeración)|Cuando es UseDefaultConfiguration `False`, un valor que indica cómo controlar los errores de clave. Los valores posibles son `ConvertToUnknown` (0) y `DiscardRecord` (1). El valor predeterminado de esta propiedad es `ConvertToUnknown` (0).|  
|KeyErrorLimit|Integer|Cuando es UseDefaultConfiguration `False`, el límite superior de los errores de clave que se permiten.|  
|KeyErrorLimitAction|Integer (enumeración)|Cuando es UseDefaultConfiguration `False`, un valor que indica la acción que se realizará cuando `KeyErrorLimit` se alcanza. Los valores posibles son `StopLogging` (1) y `StopProcessing` (0). El valor predeterminado de esta propiedad es `StopProcessing` (0).|  
|KeyErrorLogFile|String|Cuando es UseDefaultConfiguration `False`, la ruta de acceso y el nombre del archivo de registro de errores.|  
|KeyNotFound|Integer (enumeración)|Cuando es UseDefaultConfiguration `False`, un valor que indica cómo controlar la falta de errores de clave. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1), y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `ReportAndContinue` (1).|  
|NullKeyConvertedToUnknown|Integer (enumeración)|Cuando es UseDefaultConfiguration `False`, un valor que indica cómo administrar las claves null se convierte en el valor desconocido. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1), y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `IgnoreError` (0).|  
|NullKeyNotAllowed|Integer (enumeración)|Cuando es UseDefaultConfiguration `False`, un valor que indica cómo controlar valores NULL no permitidos. Los valores posibles son `IgnoreError` (0), `ReportAndContinue` (1), y `ReportAndStop` (2). El valor predeterminado de esta propiedad es `ReportAndContinue` (1).|  
|ProcessType|Integer (enumeración)|Tipo de procesamiento de particiones utilizado por la transformación. Los valores posibles son `ProcessAdd` (1) (incremental), `ProcessFull` (0) y `ProcessUpdate` (2).|  
|UseDefaultConfiguration|Boolean|Valor que especifica si la transformación usa la configuración de errores predeterminada. Si esta propiedad es `False`, la transformación utiliza los valores de las propiedades personalizadas del control de errores enumerados en esta tabla, incluidos KeyDuplicate, KeyErrorAction y así sucesivamente.|  
  
 La entrada y las columnas de entrada de destino de procesamiento de particiones no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Partition Processing Destination](partition-processing-destination.md).  
  
## <a name="see-also"></a>Vea también  
 [Common Properties](../common-properties.md)  
  
  