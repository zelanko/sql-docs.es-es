---
title: Método setMaxFieldSize (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38f7fc1d-acad-4d10-9fc8-3c0669d93b07
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8662d9e3143f61fae03c7158494015f42f4838bb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47672571"
---
# <a name="setmaxfieldsize-method-sqlserverstatement"></a>Método setMaxFieldSize (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el límite para el número máximo de bytes en una columna [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) que almacena valores de caracteres o binarios en el número establecido de bytes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setMaxFieldSize(int max)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *max*  
  
 Un valor **int** que indica el número máximo de bytes.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método setMaxFieldSize especificado por el método setMaxFieldSize en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
