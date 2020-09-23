---
title: Creación de conjuntos de filas con ICommand::Execute (controlador OLE DB) | Microsoft Docs
description: Obtenga información sobre cómo crear conjuntos de filas con ICommand::Execute en OLE DB Driver for SQL Server. Las propiedades que quiere que estén en el conjunto de filas pueden restringir el texto del comando.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
- Execute method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5a6ca010dc702471ceb932119d30ab97d249b2bf
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862251"
---
# <a name="creating-rowsets-with-icommandexecute"></a>Crear conjuntos de filas con ICommand::Execute
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En los conjuntos de filas que se crean con el método **ICommand::Execute**, las propiedades que quiera usar en el conjunto de filas resultante pueden restringir el texto del comando. Esto es especialmente importante en los consumidores que admiten texto de comando dinámico.  
  
 OLE DB Driver for SQL Server no puede usar cursores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para admitir los resultados de varios conjuntos de filas que generan muchos comandos. Si un consumidor solicita un conjunto de filas que requiere la compatibilidad con cursores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se produce un error si el texto de comando genera más de un conjunto de filas único como resultado. Para más información, consulte [Comandos que generan resultados de varios conjuntos de filas](../../oledb/ole-db-commands/commands-generating-multiple-rowset-results.md).  
  
 Los cursores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admiten conjuntos de filas de OLE DB Driver for SQL Server desplazables. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] impone limitaciones en los cursores que son sensibles a los cambios realizados por otros usuarios de la base de datos. Concretamente, las filas de algunos cursores no se pueden ordenar y es posible que no se lleve a cabo correctamente la creación de un conjunto de filas mediante un comando que contiene una cláusula SQL ORDER BY. Para obtener más información, vea [Conjuntos de filas y cursores de SQL Server](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
