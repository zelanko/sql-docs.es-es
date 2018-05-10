---
title: Propiedades personalizadas de archivo sin formato | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 66bcdd48830e2cf5b5311c34d4a8dc72b4f07ce2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="raw-file-custom-properties"></a>Propiedades personalizadas de archivo sin formato
  **Propiedades personalizadas de origen**  
  
 El origen de archivo sin formato tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen de archivo sin formato. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumeración)|Modo que se usa para tener acceso a los datos sin formato. Los valores posibles son **Nombre de archivo** (0) y **Nombre de archivo de la variable** (1). El valor predeterminado es **Nombre de archivo** (0).|  
|FileName|String|Ruta de acceso y nombre del archivo de origen.|  
  
 La salida y las columnas de salida del origen de archivo sin formato no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Raw File Source](../../integration-services/data-flow/raw-file-source.md).  
  
 **Propiedades personalizadas de los destinos**  
  
 El destino de archivo sin formato tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino de archivo sin formato. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumeración)|Valor que especifica si la propiedad FileName contiene un nombre de archivo o el nombre de una variable que contiene un nombre de archivo. Las opciones son **Nombre de archivo** (0) y **Nombre de archivo de la variable** (1).|  
|FileName|String|Nombre del archivo donde escribe el destino de archivo sin formato.|  
|WriteOption|Integer (enumeración)|Valor que especifica si el destino de archivo sin formato elimina un archivo existente que tiene el mismo nombre. Las opciones son **Crear siempre** (0), **Crear una vez** (1), **Truncar y anexar** (3) y **Anexar** (2). El valor predeterminado de esta propiedad es **Crear siempre** (0).|  
  
> [!NOTE]  
>  Una operación de anexión requiere que los metadatos de los datos anexados coincidan con los metadatos de los datos que ya están en el archivo.  
  
 La entrada y las columnas de entrada del destino de archivo sin formato no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md).  
  
## <a name="see-also"></a>Ver también  
 [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
