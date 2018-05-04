---
title: Tablas e índices | Documentos de Microsoft
description: Crear, modificar y droping tablas e índices con el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, indexes
- OLE DB, tables
- ITableDefinition interface
- tables [OLE DB]
- IIndexDefinition interface
- OLE DB Driver for SQL Server, tables
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b899fd17cd5153d7fb5624b9f6e7f25184992dc2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="tables-and-indexes"></a>Tablas e índices
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server expone la **IIndexDefinition** y **ITableDefinition** interfaces, lo que permite a los consumidores crear, modificar y quitar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tablas e índices. Las definiciones de tabla e índice válidas dependen de la versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 La capacidad de crear o quitar tablas e índices depende de los derechos de acceso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del usuario de la aplicación de consumidor. La eliminación de una tabla se puede restringir en mayor medida mediante la presencia de restricciones de integridad referencia declarativas u otros factores.  
  
 La mayoría de las aplicaciones dirigidas a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizar SQL-DMO en lugar de estos controladores OLE DB para SQL Server interfaces. SQL-DMO es una colección de objetos de OLE Automation que admite todas las funciones administrativas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Las aplicaciones con destino en varios proveedores OLE DB utilizan estas interfaces OLE DB genéricas que admiten los diferentes proveedores OLE DB.  
  
 En el conjunto de propiedades específico de proveedor DBPROPSET_SQLSERVERCOLUMN, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] define la propiedad siguiente.  
  
|Id. de propiedad|Description|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|Tipo: VT_BSTR<br /><br /> L/E: escritura<br /><br /> Valor predeterminado: NULL<br /><br /> Descripción: Esta propiedad solo se utiliza en **ITableDefinition**. La cadena especificada en esta propiedad se utiliza para crear un [CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md)<br /><br /> .|  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Crear tablas de SQL Server](../../oledb/ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [Agregar una columna a una tabla de SQL Server](../../oledb/ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [Quitar una columna de una tabla de SQL Server](../../oledb/ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [Quitar una tabla de SQL Server](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [Creación de índices de SQL Server](../../oledb/ole-db-tables-indexes/creating-sql-server-indexes.md)  
  
-   [Quitar un índice de SQL Server](../../oledb/ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para la programación de SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [Eliminar tabla & #40; Transact-SQL & #41;](../../../t-sql/statements/drop-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/create-index-transact-sql.md)   
 [DROP INDEX &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-index-transact-sql.md)  
  
  
