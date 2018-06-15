---
title: 'Crear conjuntos de filas con ICommand:: Execute | Documentos de Microsoft'
description: 'Crear conjuntos de filas con ICommand:: Execute'
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
- Execute method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 546cd4cc752fb89172dc9683f6ce8eac448cf7f9
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35305324"
---
# <a name="creating-rowsets-with-icommandexecute"></a>Crear conjuntos de filas con ICommand::Execute
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para conjuntos de filas que se crean mediante el **ICommand:: Execute** método, las propiedades que desea incluir en el conjunto de filas resultante puede restringir el texto del comando. Esto es especialmente importante en los consumidores que admiten texto de comando dinámico.  
  
 No se puede usar el controlador OLE DB para SQL Server [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cursores para admitir los resultados de varios conjuntos de filas generados por muchos comandos. Si un consumidor solicita un conjunto de filas que requiere la compatibilidad con cursores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se produce un error si el texto de comando genera más de un conjunto de filas único como resultado. Para obtener más información, consulte [resultados de varios conjuntos de filas de generación de comandos](../../oledb/ole-db-commands/commands-generating-multiple-rowset-results.md).  
  
 Desplazable controlador OLE DB para conjuntos de filas de SQL Server son compatibles con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] los cursores. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] impone limitaciones en los cursores que son sensibles a los cambios realizados por otros usuarios de la base de datos. Concretamente, las filas de algunos cursores no se pueden ordenar y es posible que no se lleve a cabo correctamente la creación de un conjunto de filas mediante un comando que contiene una cláusula SQL ORDER BY. Para obtener más información, consulte [conjuntos de filas y cursores de servidor SQL](../../oledb/ole-db-rowsets/rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
