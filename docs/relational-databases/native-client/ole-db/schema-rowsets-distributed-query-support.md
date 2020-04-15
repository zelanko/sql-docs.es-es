---
title: Compatibilidad con consultas distribuidas en conjuntos de filas de esquema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- DBPROPSET_SQLSERVERSESSION property
- schema rowsets [OLE DB]
- distributed queries [SQL Server], SQL Server Native Client OLE DB provider
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- rowsets [OLE DB], schema
ms.assetid: 11354bb6-be42-4d8d-854c-42dd3dc38656
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: daf4f4c0c7c6c1d53c2ab899dd150756399d53a3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297015"
---
# <a name="schema-rowsets---distributed-query-support"></a>Conjuntos de filas de esquema: compatibilidad con consultas distribuidas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admitir consultas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] distribuidas, la interfaz **IDBSchemaRowset** del proveedor OLE DB de Native Client devuelve metadatos en servidores vinculados.  
  
 Si la propiedad SSPROP_QUOTEDCATALOGNAMES de DBPROPSET_SQLSERVERSESSION es VARIANT_TRUE, puede especificarse un identificador entrecomillado para el nombre del catálogo (por ejemplo, "my.catalog"). Al restringir la salida del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conjunto de filas de esquema por catálogo, el proveedor OLE DB de Native Client reconoce un nombre de dos partes que contiene el nombre de catálogo y servidor vinculado. Para los conjuntos de filas de esquema de la tabla siguiente, especificando un nombre de catálogo de dos partes como _linked_server_**.** _catálogo_ restringe la salida al catálogo aplicable del servidor vinculado con nombre.  
  
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
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client define el conjunto de filas de esquema LINKEDSERVERS, devolviendo una lista de orígenes de datos OLE DB registrados como servidores vinculados.  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad con conjuntos de filas de esquema &#40;&#41;OLE DB](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [LINKEDSERVERS Rowset &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
