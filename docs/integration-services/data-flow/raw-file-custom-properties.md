---
description: Propiedades personalizadas de archivo sin formato
title: Propiedades personalizadas de archivo sin formato | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7e81f7e1-fac0-4b57-b145-8f1b9e4720bf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5b1b7f0e1416b20ce641848abe47d3497f7c7b7f
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196413"
---
# <a name="raw-file-custom-properties"></a>Propiedades personalizadas de archivo sin formato

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **Propiedades personalizadas de origen**  
  
 El origen de archivo sin formato tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del origen de archivo sin formato. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumeración)|Modo que se usa para tener acceso a los datos sin formato. Los valores posibles son **Nombre de archivo** (0) y **Nombre de archivo de la variable** (1). El valor predeterminado es **Nombre de archivo** (0).|  
|FileName|String|Ruta de acceso y nombre del archivo de origen.|  
  
 La salida y las columnas de salida del origen de archivo sin formato no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Raw File Source](../../integration-services/data-flow/raw-file-source.md).  
  
 **Propiedades personalizadas de los destinos**  
  
 El destino de archivo sin formato tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino de archivo sin formato. Todas las propiedades son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (enumeración)|Valor que especifica si la propiedad FileName contiene un nombre de archivo o el nombre de una variable que contiene un nombre de archivo. Las opciones son **Nombre de archivo** (0) y **Nombre de archivo de la variable** (1).|  
|FileName|String|Nombre del archivo donde escribe el destino de archivo sin formato.|  
|WriteOption|Integer (enumeración)|Valor que especifica si el destino de archivo sin formato elimina un archivo existente que tiene el mismo nombre. Las opciones son **Crear siempre** (0), **Crear una vez** (1), **Truncar y anexar** (3) y **Anexar** (2). El valor predeterminado de esta propiedad es **Crear siempre** (0).|  
  
> [!NOTE]  
>  Una operación de anexión requiere que los metadatos de los datos anexados coincidan con los metadatos de los datos que ya están en el archivo.  
  
 La entrada y las columnas de entrada del destino de archivo sin formato no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [Raw File Destination](../../integration-services/data-flow/raw-file-destination.md).  
  
## <a name="see-also"></a>Vea también  
 [Common Properties](./set-the-properties-of-a-data-flow-component.md)  
  
