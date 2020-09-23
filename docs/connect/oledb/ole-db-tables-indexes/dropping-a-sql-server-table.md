---
title: Eliminación de una tabla de SQL Server (controlador OLE DB) | Microsoft Docs
description: Obtenga información sobre cómo quitar una tabla de SQL Server desde una base de datos mediante el uso de la función ITableDefinition::DropTable en OLE DB Driver for SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- OLE DB Driver for SQL Server, tables
- removing tables
- dropping tables
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3bdcc2b2b96c2cd1d9af0bbf7d31457eed71381
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859408"
---
# <a name="dropping-a-sql-server-table"></a>Quitar una tabla de SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server expone la función **ITableDefinition::DropTable** para quitar una tabla de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de una base de datos.  
  
 Especifique el nombre de la tabla como una cadena de caracteres Unicode en el miembro *pwszName* de la unión *uName* en el parámetro *pTableID*. El miembro *eKind* de *pTableID* debe ser DBKIND_NAME.  
  
## <a name="see-also"></a>Consulte también  
 [Tablas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  
