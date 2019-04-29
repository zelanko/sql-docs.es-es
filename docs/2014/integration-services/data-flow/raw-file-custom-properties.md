---
title: Propiedades personalizadas de archivo sin formato | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fe3f77ac629aab7534077274aa9cf62a50149b57
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900905"
---
# <a name="raw-file-custom-properties"></a>Propiedades personalizadas de archivo sin formato
  **Propiedades personalizadas de origen**  
  
 El origen de archivo sin formato tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen de archivo sin formato. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumeración)|Modo que se usa para tener acceso a los datos sin formato. Los valores posibles son `File name` (0) y `File name from variable` (1). El valor predeterminado es `File name` (0).|  
|FileName|String|Ruta de acceso y nombre del archivo de origen.|  
  
 La salida y las columnas de salida del origen de archivo sin formato no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Raw File Source](raw-file-source.md).  
  
 **Propiedades personalizadas de los destinos**  
  
 El destino de archivo sin formato tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino de archivo sin formato. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumeración)|Valor que especifica si la propiedad FileName contiene un nombre de archivo o el nombre de una variable que contiene un nombre de archivo. Las opciones son `File name` (0) y `File name from variable` (1).|  
|FileName|String|Nombre del archivo donde escribe el destino de archivo sin formato.|  
|WriteOption|Integer (enumeración)|Valor que especifica si el destino de archivo sin formato elimina un archivo existente que tiene el mismo nombre. Las opciones son `Create Always` (0), `Create Once` (1), `Truncate and Append` (3) y `Append` (2). El valor predeterminado de esta propiedad es `Create Always` (0).|  
  
> [!NOTE]  
>  Una operación de anexión requiere que los metadatos de los datos anexados coincidan con los metadatos de los datos que ya están en el archivo.  
  
 La entrada y las columnas de entrada del destino de archivo sin formato no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Raw File Destination](raw-file-destination.md).  
  
## <a name="see-also"></a>Vea también  
 [Common Properties](../common-properties.md)  
  
  
