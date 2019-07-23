---
title: Método isValid (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3915690475e5ce9321af7fc15498c2bde018c640
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977130"
---
# <a name="isvalid-method-sqlserverconnection"></a>Método isValid (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica si este objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) se ha cerrado y si sigue siendo válido.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *timeout*  
  
 Un valor **int** que especifica el número de segundos que transcurrirán antes de que se valide la conexión.  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si la conexión es válida; **false** si la conexión no es válida o no se puede determinar la validez de la conexión antes de que expire el tiempo de espera.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método IsValid especifica este método isValid en la interfaz java. SQL. Connection.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
