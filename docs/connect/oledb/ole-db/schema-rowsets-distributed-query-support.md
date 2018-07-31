---
title: Compatibilidad con consultas de conjuntos de filas de esquema distribuidas | Microsoft Docs
description: Compatibilidad con consultas distribuidas en conjuntos de filas de esquema
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], OLE DB Driver for SQL Server
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 085a4424272e4d620c4b36fe9ecf44894cb1a33f
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39105831"
---
# <a name="schema-rowsets---distributed-query-support"></a>Conjuntos de filas de esquema: compatibilidad con consultas distribuidas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Para admitir consultas distribuidas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la interfaz **IDBSchemaRowset** del controlador OLE DB para SQL Server devuelve metadatos en servidores vinculados.  
  
 Si la propiedad SSPROP_QUOTEDCATALOGNAMES de DBPROPSET_SQLSERVERSESSION es VARIANT_TRUE, puede especificarse un identificador entrecomillado para el nombre del catálogo (por ejemplo, "my.catalog"). Al restringir los resultados del conjunto de filas de esquema por catálogo, el controlador OLE DB para SQL Server reconoce un nombre de dos partes que contiene el nombre del servidor vinculado y del catálogo. Para los conjuntos de filas de esquema que figuran en la siguiente tabla, especificar un nombre de catálogo de dos partes, como *linked_server ***.*** catalog* restringe los resultados al catálogo aplicable del servidor con nombre vinculado.  
  
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
>  Para restringir un conjunto de filas de esquema a todos los catálogos de un servidor vinculado, use la sintaxis *linked_server* (donde el separador de punto forma parte de la especificación del nombre). Esta sintaxis equivale a especificar NULL para la restricción del nombre de catálogo y también se utiliza cuando el servidor vinculado indica un origen de datos que no admite catálogos.  
  
 El controlador OLE DB para SQL Server define el conjunto de filas de esquema LINKEDSERVERS y devuelve una lista de los orígenes de datos OLE DB registrados como servidores vinculados.  
  
## <a name="see-also"></a>Ver también  
 [Compatibilidad con conjuntos de filas de esquema &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowset-support-ole-db.md)   
 [Conjunto de filas LINKEDSERVERS &#40;OLE DB&#41;](../../oledb/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
