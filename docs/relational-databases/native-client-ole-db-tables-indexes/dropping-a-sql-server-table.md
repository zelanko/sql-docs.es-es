---
title: Eliminación de una tabla de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- SQL Server Native Client OLE DB provider, tables
- removing tables
- dropping tables
ms.assetid: b6d6c4de-43c6-473e-92aa-34ffddd58cbe
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b6ae20812f7ebd9815d8cc010d5e2a24e994c75a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280054"
---
# <a name="dropping-a-sql-server-table"></a>Quitar una tabla de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client expone la función [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ITableDefinition::DropTable** para quitar una tabla de una base de datos.  
  
 Especifique el nombre de la tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
## <a name="see-also"></a>Consulte también  
 [Tablas e índices](../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
  
