---
title: Método isValid (SQLServerConnection) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 3b0a8bbf-9369-4456-9ab8-1434ccacdd7e
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8c1e65ecb40137e0da2de7abd8b5d40e7e744752
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="isvalid-method-sqlserverconnection"></a>Método isValid (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica si este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto no se ha cerrado y sigue siendo válido.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isValid(int timeout)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Tiempo de espera*  
  
 Un **int** que especifica el número de segundos de espera para validar la conexión.  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si la conexión es válida; **false** si la conexión no es válida o no se puede determinar la validez de la conexión antes de que expire el tiempo de espera.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método isValid especificado por el método isValid en la interfaz java.sql.Connection.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
