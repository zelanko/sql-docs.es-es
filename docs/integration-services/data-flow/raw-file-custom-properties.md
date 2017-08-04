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
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a364ae62ebc8823f9d57fb44ef99b7b14469c608
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="raw-file-custom-properties"></a>Propiedades personalizadas de archivo sin formato
  **Propiedades personalizadas de origen**  
  
 El origen de archivo sin formato tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen de archivo sin formato. Todas las propiedades son de lectura y escritura.  
  
|Nombre de la propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumeración)|Modo que se usa para tener acceso a los datos sin formato. Los valores posibles son **Nombre de archivo** (0) y **Nombre de archivo de la variable** (1). El valor predeterminado es **Nombre de archivo** (0).|  
|FileName|String|Ruta de acceso y nombre del archivo de origen.|  
  
 La salida y las columnas de salida del origen de archivo sin formato no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Raw File Source](../../integration-services/data-flow/raw-file-source.md).  
  
 **Propiedades personalizadas de los destinos**  
  
 El destino de archivo sin formato tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino de archivo sin formato. Todas las propiedades son de lectura y escritura.  
  
|Nombre de la propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumeración)|Valor que especifica si la propiedad FileName contiene un nombre de archivo o el nombre de una variable que contiene un nombre de archivo. Las opciones son **Nombre de archivo** (0) y **Nombre de archivo de la variable** (1).|  
|FileName|String|Nombre del archivo donde escribe el destino de archivo sin formato.|  
|WriteOption|Integer (enumeración)|Valor que especifica si el destino de archivo sin formato elimina un archivo existente que tiene el mismo nombre. Las opciones son **Crear siempre** (0), **Crear una vez** (1), **Truncar y anexar** (3) y **Anexar** (2). El valor predeterminado de esta propiedad es **Crear siempre** (0).|  
  
> [!NOTE]  
>  Una operación de anexión requiere que los metadatos de los datos anexados coincidan con los metadatos de los datos que ya están en el archivo.  
  
 La entrada y las columnas de entrada del destino de archivo sin formato no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
