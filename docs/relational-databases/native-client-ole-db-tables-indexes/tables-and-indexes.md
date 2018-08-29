---
title: Las tablas e índices | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, indexes
- OLE DB, tables
- ITableDefinition interface
- tables [OLE DB]
- IIndexDefinition interface
- SQL Server Native Client OLE DB provider, tables
- SQL Server Native Client OLE DB provider, indexes
- indexes [OLE DB]
ms.assetid: 4217c6d8-8cd2-43dc-b36f-3cfd8a58fabc
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 690c930ea778d0d8480b8e6d1899207101d9740d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43069205"
---
# <a name="tables-and-indexes"></a>Tablas e índices
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **IIndexDefinition** y **ITableDefinition** interfaces, lo que permite a los consumidores crear, modificar y quitar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas y índices. Las definiciones de tabla e índice válidas dependen de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La capacidad de crear o quitar tablas e índices depende de los derechos de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del usuario de la aplicación de consumidor. La eliminación de una tabla se puede restringir en mayor medida mediante la presencia de restricciones de integridad referencia declarativas u otros factores.  
  
 La mayoría de las aplicaciones destinadas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizar SQL-DMO en lugar de estas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces del proveedor OLE DB de Native Client. SQL-DMO es una colección de objetos de OLE Automation que admite todas las funciones administrativas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las aplicaciones con destino en varios proveedores OLE DB utilizan estas interfaces OLE DB genéricas que admiten los diferentes proveedores OLE DB.  
  
 En el conjunto de propiedades específico de proveedor DBPROPSET_SQLSERVERCOLUMN, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define la propiedad siguiente.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|Tipo: VT_BSTR<br /><br /> L/E: escritura<br /><br /> Valor predeterminado: NULL<br /><br /> Descripción: esta propiedad solo se usa en **ITableDefinition**. La cadena especificada en esta propiedad se usa al crear una instrucción [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md).<br /><br /> .|  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Crear tablas de SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [Agregar una columna a una tabla de SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [Quitar una columna de una tabla de SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [Quitar una tabla de SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [Crear índices de SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [Quitar un índice de SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
  
