---
title: 'Crear conjuntos de filas con ICommand:: Execute | Documentos de Microsoft'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
- Execute method
ms.assetid: 9b530b7d-8165-49d4-a978-5ced17c6705e
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b62e32653777192d77c404cabee49cc188444204
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200114"
---
# <a name="creating-rowsets-with-icommandexecute"></a>Crear conjuntos de filas con ICommand::Execute
  Para conjuntos de filas que se crean mediante el **ICommand:: Execute** método, las propiedades que desea incluir en el conjunto de filas resultante puede restringir el texto del comando. Esto es especialmente importante en los consumidores que admiten texto de comando dinámico.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede usar el proveedor OLE DB de Native Client [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores para admitir los resultados de varios conjuntos de filas generados por muchos comandos. Si un consumidor solicita un conjunto de filas que requiere la compatibilidad con cursores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se produce un error si el texto de comando genera más de un conjunto de filas único como resultado. Para obtener más información, consulte [resultados de varios conjuntos de filas de generación de comandos](../native-client-ole-db-commands/commands-generating-multiple-rowset-results.md).  
  
 Desplazable [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten conjuntos de filas de proveedor OLE DB de Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impone limitaciones en los cursores que son sensibles a los cambios realizados por otros usuarios de la base de datos. Concretamente, las filas de algunos cursores no se pueden ordenar y es posible que no se lleve a cabo correctamente la creación de un conjunto de filas mediante un comando que contiene una cláusula SQL ORDER BY. Para obtener más información, consulte [conjuntos de filas y cursores de servidor SQL](rowsets-and-sql-server-cursors.md).  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](rowsets.md)  
  
  