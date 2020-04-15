---
title: Creación de conjuntos de filas con ICommand::Execute | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
- Execute method
ms.assetid: 9b530b7d-8165-49d4-a978-5ced17c6705e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0658928bcf1e4ee5fd67e3c934cd589cc13a28b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286855"
---
# <a name="creating-rowsets-with-icommandexecute"></a>Crear conjuntos de filas con ICommand::Execute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  En los conjuntos de filas que se crean con el método **ICommand::Execute**, las propiedades que quiera usar en el conjunto de filas resultante pueden restringir el texto del comando. Esto es especialmente importante en los consumidores que admiten texto de comando dinámico.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Native Client no puede usar cursores para admitir los resultados de varios conjuntos de filas generados por muchos comandos. Si un consumidor solicita un conjunto de filas que requiere la compatibilidad con cursores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se produce un error si el texto de comando genera más de un conjunto de filas único como resultado. Para más información, consulte [Comandos que generan resultados de varios conjuntos de filas](../../relational-databases/native-client-ole-db-commands/commands-generating-multiple-rowset-results.md).  
  
 Los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores admiten conjuntos de filas de proveedor OLE DB de Native Client desplazables. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impone limitaciones en los cursores que son sensibles a los cambios realizados por otros usuarios de la base de datos. Concretamente, las filas de algunos cursores no se pueden ordenar y es posible que no se lleve a cabo correctamente la creación de un conjunto de filas mediante un comando que contiene una cláusula SQL ORDER BY. Para obtener más información, vea [Conjuntos de filas y cursores de SQL Server](../../relational-databases/native-client-ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
