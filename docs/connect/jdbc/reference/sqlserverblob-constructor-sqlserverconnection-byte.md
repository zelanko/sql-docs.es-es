---
title: Constructor SQLServerBlob (SQLServerConnection, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: aff7392d2aceab631e5e53cd446696f8ce15ab43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66773094"
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
  
## <a name="see-also"></a>Consulte también  
 [Constructores SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [Miembros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
