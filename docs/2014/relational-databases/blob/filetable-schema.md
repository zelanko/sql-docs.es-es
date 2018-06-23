---
title: Esquema de FileTable | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FileTables [SQL Server], table schema
ms.assetid: e1cb3880-cfda-40ac-91fc-d08998287f44
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8515d78ddab2dd39e223087a44b0e021a5aca439
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204627"
---
# <a name="filetable-schema"></a>Esquema de FileTable
  Describe los esquemas predefinido y fijo de una FileTable.  
  
|Nombre de atributo de archivo|Tipo|Tamaño|Valor predeterminado|Descripción|Accesibilidad del sistema de archivos|  
|-------------------------|----------|----------|-------------|-----------------|-------------------------------|  
|**path_locator**|`hierarchyid`|variable|Un `hierarchyid` que identifica la posición de este elemento.|La posición de este nodo en el objeto FileNamespace jerárquico.<br /><br /> La clave principal de la tabla.|Se puede crear y modificar estableciendo los valores de la ruta de acceso de Windows.|  
|**stream_id**|**[uniqueidentifier] rowguidcol**||Un valor devuelto por la `NEWID()` (función).|Identificador único de los datos de FILESTREAM.|No aplicable.|  
|**file_stream**|`varbinary(max)`<br /><br /> `filestream`|variable|NULL|Contiene los datos de FILESTREAM.|No aplicable.|  
|**file_type**|`nvarchar(255)`|variable|NULL.<br /><br /> Una operación de creación o cambio de nombre del sistema de archivos rellena el valor de la extensión de archivo a partir del nombre.|Representa el tipo de archivo.<br /><br /> Esta columna se puede usar como `TYPE COLUMN` cuando se crea un índice de texto completo.<br /><br /> **file_type** es una columna calculada persistente.|Calculado automáticamente. No se puede establecer.|  
|**Nombre**|`nvarchar(255)`|variable|Valor de GUID.|El nombre de archivo o de directorio.|Se puede crear o modificar mediante las API de Windows.|  
|**parent_path_locator**|`hierarchyid`|variable|`hierarchyid` que identifica el directorio que contiene este elemento.|El `hierarchyid` del directorio contenedor.<br /><br /> **parent_path_locator** es una columna calculada persistente.|Calculado automáticamente. No se puede establecer.|  
|**cached_file_size**|`bigint`|||El tamaño en bytes de los datos FILESTREAM.<br /><br /> **cached_file_size** es una columna calculada persistente.|Aunque el tamaño del archivo almacenado en memoria caché se mantenga actualizado automáticamente, puede perder la sincronización en circunstancias inusuales. Para calcular el tamaño exacto, use la `DATALENGTH()` función.|  
|**creation_time**|`datetime2(4)`<br /><br /> `not null`|8 bytes|Tiempo actual.|Fecha y hora de creación del archivo.|Calculado automáticamente. También se puede establecer con las API de Windows.|  
|**last_write_time**|`datetime2(4)`<br /><br /> `not null`|8 bytes|Tiempo actual.|Fecha y hora en que se modificó por última vez el archivo.|Calculado automáticamente. También se puede establecer con las API de Windows.|  
|**last_access_time**|`datetime2(4)`<br /><br /> `not null`|8 bytes|Tiempo actual.|Fecha y hora en que se obtuvo acceso por última vez al archivo.|Calculado automáticamente. También se puede establecer con las API de Windows.|  
|**is_directory**|`bit`<br /><br /> `not null`|1 byte|FALSE|Indica si la fila representa un directorio. Este valor se calcula automáticamente y no se puede establecer.|Calculado automáticamente. No se puede establecer.|  
|**is_offline**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de archivo sin conexión.|Calculado automáticamente. También se puede establecer con las API de Windows.|  
|**is_hidden**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de archivo oculto.|Calculado automáticamente. También se puede establecer con las API de Windows.|  
|**is_readonly**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de archivo de solo lectura.|Calculado automáticamente. También se puede establecer con las API de Windows.|  
|**is_archive**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de archivo.|Calculado automáticamente. También se puede establecer con las API de Windows.|  
|**is_system**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de archivo del sistema.|Calculado automáticamente. También se puede establecer con las API de Windows.|  
|**is_temporary**|`bit`<br /><br /> `not null`|1 byte|FALSE|Atributo de archivo temporal.|Calculado automáticamente. También se puede establecer con las API de Windows.|  
  
## <a name="see-also"></a>Vea también  
 [Crear, modificar y quitar FileTables](create-alter-and-drop-filetables.md)  
  
  