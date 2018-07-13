---
title: Compatibilidad con consultas de conjuntos de filas de esquema distribuidas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b640761d4c88f5a6a93772e12a2249f9f88f28f5
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419764"
---
# <a name="distributed-query-support-in-schema-rowsets"></a>Compatibilidad con consultas distribuidas en conjuntos de filas de esquema
  Para admitir [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consultas distribuidas, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB **IDBSchemaRowset** interfaz devuelve los metadatos para los servidores vinculados.  
  
 Si la propiedad SSPROP_QUOTEDCATALOGNAMES de DBPROPSET_SQLSERVERSESSION es VARIANT_TRUE, puede especificarse un identificador entrecomillado para el nombre del catálogo (por ejemplo, "my.catalog"). Al restringir la salida del conjunto de filas de esquema por catálogo, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client reconoce un nombre de dos partes que contiene el nombre de catálogo y el servidor vinculado. Para los conjuntos de filas de esquema en la tabla siguiente, especificando un nombre de catálogo de dos partes como *linked_server ***.*** catálogo* restringe la salida al catálogo aplicable del servidor vinculado con nombre.  
  
|Conjunto de filas de esquema|Restricción de catálogo|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMNS|TABLE_CATALOG|  
|DBSCHEMA_PRIMARY_KEYS|TABLE_CATALOG|  
|DBSCHEMA_TABLES|TABLE_CATALOG|  
|DBSCHEMA_FOREIGN_KEYS|PK_TABLE_CATALOG FK_TABLE_CATALOG|  
|DBSCHEMA_INDEXES|TABLE_CATALOG|  
|DBSCHEMA_COLUMN_PRIVILEGES|TABLE_CATALOG|  
|DBSCHEMA_TABLE_PRIVILEGES|TABLE_CATALOG|  
  
> [!NOTE]  
>  Para restringir un conjunto de filas de esquema a todos los catálogos de un servidor vinculado, utilice la sintaxis *linked_server* (donde el separador punto forma parte de la especificación de nombre). Esta sintaxis equivale a especificar NULL para la restricción del nombre de catálogo y también se utiliza cuando el servidor vinculado indica un origen de datos que no admite catálogos.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client define el conjunto de filas de esquema LINKEDSERVERS y devuelve una lista de orígenes de datos OLE DB registrados como servidores vinculados.  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con el conjunto de filas de esquema &#40;OLE DB&#41;](schema-rowset-support-ole-db.md)   
 [Conjunto de filas LINKEDSERVERS &#40;OLE DB&#41;](schema-rowsets-linkedservers-rowset.md)  
  
  
