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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d3c162bbcbf9f9212d6adc3838a06b5eaaac8b13
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73759711"
---
# <a name="schema-rowsets---distributed-query-support"></a>Conjuntos de filas de esquema: compatibilidad con consultas distribuidas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para admitir [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las consultas distribuidas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , la interfaz **IDBSchemaRowset** del proveedor de OLE DB de Native Client devuelve metadatos en servidores vinculados.  
  
 Si la propiedad SSPROP_QUOTEDCATALOGNAMES de DBPROPSET_SQLSERVERSESSION es VARIANT_TRUE, puede especificarse un identificador entrecomillado para el nombre del catálogo (por ejemplo, "my.catalog"). Al restringir la salida del conjunto de filas de esquema [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por catálogo, el proveedor de OLE DB de Native Client reconoce un nombre de dos partes que contiene el nombre del servidor vinculado y del catálogo. Para los conjuntos de filas de esquema en la tabla siguiente, especifique un nombre de catálogo de dos partes como _linked_server_**.** _Catalog_ restringe la salida al catálogo aplicable del servidor vinculado con nombre.  
  
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
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client define el conjunto de filas de esquema LINKEDSERVERS, y devuelve una lista de OLE DB orígenes de datos registrados como servidores vinculados.  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad de conjunto de filas de esquema &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)   
 [&#40;de conjunto de filas LINKEDSERVERS OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowsets-linkedservers-rowset.md)  
  
  
