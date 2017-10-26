---
title: Propiedades personalizadas de archivo sin formato | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 097c9a07d738bb1b192095ac91448487fdfa0eb1
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="flat-file-custom-properties"></a>Propiedades personalizadas de archivo plano
  **Propiedades personalizadas de origen**  
  
 El origen de archivo plano tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen de archivo plano. Todas las propiedades son de lectura y escritura.  
  
|Nombre de la propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|String|Nombre de una columna de salida que contiene el nombre de archivo. Si no se especifica ningún nombre, se generará ninguna columna de salida que contenga el nombre de archivo.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de origen de archivos planos**, pero se puede establecer mediante el **Editor avanzado**.|  
|RetainNulls|Boolean|Valor que especifica si retener los valores Null del archivo de origen como tales cuando el motor de canalización de transformación de datos procesa los datos. El valor predeterminado de esta propiedad es **False**.|  
  
 La salida del origen de archivo plano no tiene ninguna propiedad personalizada.  
  
 En la tabla siguiente se describen las propiedades personalizadas de las columnas de salida del origen de archivo plano. Todas las propiedades son de lectura y escritura.  
  
|Nombre de la propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|FastParse|Boolean|Valor que indica si la columna usa las rutinas de análisis más rápidas que no distinguen la configuración regional y permiten un análisis rápido que DTS proporciona, o las rutinas de análisis estándar que sí distinguen la configuración regional. Para obtener más información, consulte [Fast Parse](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95) y [Standard Parse](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013). El valor predeterminado de esta propiedad es **False**.<br /><br /> Nota: Esta propiedad no está disponible en el **Editor de origen de archivos planos**, pero se puede establecer mediante el **Editor avanzado**.|  
  
 Para más información, consulte [Flat File Source](../../integration-services/data-flow/flat-file-source.md).  
  
 **Propiedades personalizadas de los destinos**  
  
 El destino de archivo plano tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino Archivo plano. Todas las propiedades son de lectura y escritura.  
  
|Nombre de la propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|Encabezado|String|Bloque de texto que se inserta en el archivo antes de que se escriban datos.<br /><br /> Puede especificar el valor de esta propiedad con una expresión de propiedad.|  
|Sobrescribir|Boolean|Valor que especifica si sobrescribir o anexar a un archivo de destino existente que tiene el mismo nombre. El valor predeterminado de esta propiedad es **True**.|  
  
 La entrada y las columnas de entrada del destino de archivo plano no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Flat File Destination](../../integration-services/data-flow/flat-file-destination.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  

