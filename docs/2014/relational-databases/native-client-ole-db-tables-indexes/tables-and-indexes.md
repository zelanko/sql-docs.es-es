---
title: Tablas e índices | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
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
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 14e7c96e5157853ae3ae93f3ac276d566ed18ae2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204391"
---
# <a name="tables-and-indexes"></a>Tablas e índices
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la **IIndexDefinition** y **ITableDefinition** interfaces, lo que permite a los consumidores crear, modificar y quitar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas y índices. Las definiciones de tabla e índice válidas dependen de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La capacidad de crear o quitar tablas e índices depende de los derechos de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del usuario de la aplicación de consumidor. La eliminación de una tabla se puede restringir en mayor medida mediante la presencia de restricciones de integridad referencia declarativas u otros factores.  
  
 La mayoría de las aplicaciones dirigidas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizar SQL-DMO en lugar de estas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interfaces del proveedor OLE DB de Native Client. SQL-DMO es una colección de objetos de OLE Automation que admite todas las funciones administrativas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las aplicaciones con destino en varios proveedores OLE DB utilizan estas interfaces OLE DB genéricas que admiten los diferentes proveedores OLE DB.  
  
 En el conjunto de propiedades específico de proveedor DBPROPSET_SQLSERVERCOLUMN, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define la propiedad siguiente.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_COL_COLLATIONNAME|Tipo: VT_BSTR<br /><br /> L/E: escritura<br /><br /> Valor predeterminado: NULL<br /><br /> Descripción: Esta propiedad solo se utiliza en **ITableDefinition**. La cadena especificada en esta propiedad se utiliza para crear un [CREATE TABLE](/sql/t-sql/statements/create-table-transact-sql)<br /><br /> .|  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Crear tablas de SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/creating-sql-server-tables.md)  
  
-   [Agregar una columna a una tabla de SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/adding-a-column-to-a-sql-server-table.md)  
  
-   [Quitar una columna de una tabla de SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/removing-a-column-from-a-sql-server-table.md)  
  
-   [Quitar una tabla de SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/dropping-a-sql-server-table.md)  
  
-   [Crear índices de SQL Server](../../relational-databases/indexes/indexes.md)  
  
-   [Quitar un índice de SQL Server](../../relational-databases/native-client-ole-db-tables-indexes/dropping-a-sql-server-index.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [DROP TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-table-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
  
