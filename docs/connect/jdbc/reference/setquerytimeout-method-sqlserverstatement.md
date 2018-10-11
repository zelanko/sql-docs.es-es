---
title: Método setQueryTimeout (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0c513265-cd0c-4b38-9494-94458c17a16d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09c984b0d4a0bfa1fedb57f60532a721b16afccf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47621404"
---
# <a name="setquerytimeout-method-sqlserverstatement"></a>Método setQueryTimeout (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el número de segundos que esperará el controlador antes de que se ejecute un objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) según el número de segundos determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setQueryTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *segundos*  
  
 Un valor **int** que indica el número de segundos que transcurrirán; se establece en 0 si no hay límite alguno.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método setQueryTimeout especificado por el método setQueryTimeout en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
