---
title: Resultados del mensaje de SQL Server | Documentos de Microsoft
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
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 7d1f6519c927bc8050590c1cc13821a7b7895f8a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108324"
---
# <a name="sql-server-message-results"></a>Resultados de los mensajes de SQL Server
  El siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones no generar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de filas de proveedor OLE DB de Native Client o un recuento de filas afectadas al ejecutarse:  
  
-   PRINT  
  
-   RAISERROR con una gravedad de 10 o inferior  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instrucciones devuelven uno o varios mensajes informativos o hacen que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelva mensajes informativos en lugar de resultados de conjunto de filas o de recuento. En la ejecución correcta, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve S_OK y los mensajes están disponibles para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client devuelve S_OK y tiene uno o más mensajes informativos disponibles después de la ejecución de muchos [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones o la ejecución del consumidor de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] miembro del proveedor OLE DB de Native Client función.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor OLE DB de Native Client que permite la especificación dinámica de texto de la consulta debe comprobar interfaces de error después de cada ejecución de la función miembro independientemente del valor de código de retorno, la presencia o ausencia de un devuelto**IRowset** o **IMultipleResults** referencia de la interfaz o un recuento de filas afectadas.  
  
## <a name="see-also"></a>Vea también  
 [Errores](errors.md)  
  
  