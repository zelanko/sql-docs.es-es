---
title: Resultados de mensajes de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: rothja
ms.author: jroth
ms.openlocfilehash: aa63445b81ec89b87523fa29c50817e128d48515
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85043564"
---
# <a name="sql-server-message-results"></a>Resultados de los mensajes de SQL Server
  Las [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones siguientes no generan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de filas de proveedor de OLE DB de cliente nativo ni un recuento de las filas afectadas cuando se ejecutan:  
  
-   PRINT  
  
-   RAISERROR con una gravedad de 10 o inferior  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instrucciones devuelven uno o varios mensajes informativos o hacen que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelva mensajes informativos en lugar de resultados de conjunto de filas o de recuento. Al ejecutarse correctamente, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client devuelve S_OK y los mensajes están disponibles para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor de OLE DB de Native Client.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client devuelve S_OK y tiene uno o más mensajes informativos disponibles después de la ejecución de muchas [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones o la ejecución del consumidor de una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] función miembro de proveedor de OLE DB de Native Client.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor del proveedor de OLE DB de Native Client que permite la especificación dinámica del texto de la consulta debe comprobar las interfaces de error después de cada ejecución de función miembro independientemente del valor del código de retorno, la presencia o ausencia de una referencia de interfaz **IRowset** o **IMultipleResults** devuelta, o un recuento de filas afectadas.  
  
## <a name="see-also"></a>Consulte también  
 [Errores](errors.md)  
  
  
