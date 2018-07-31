---
title: Constructor SQLServerBlob (SQLServerConnection, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d93e5bee03976c5ae9c55247f98ba180e237a4e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38064418"
---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>Constructor SQLServerBlob (SQLServerConnection, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa una nueva instancia de la clase [SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md) cuando se proporcionan un objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) y una matriz **byte**.  
  
> [!NOTE]  
>  Este método se ha dejado de utilizar en la versión 2.0 del controlador JDBC. En su lugar, se usa el método [createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *connection*  
  
 Objeto SQLServerConnection.  
  
 *data*  
  
 Matriz **byte**.  
  
## <a name="see-also"></a>Ver también  
 [Constructores SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [Miembros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
