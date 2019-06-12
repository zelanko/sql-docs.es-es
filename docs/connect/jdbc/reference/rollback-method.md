---
title: Método Rollback () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.rollback ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7adb6772-4047-4d8e-931d-b3d20eec44b5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d58c91b4e305eaabeef11b995a16378441d659fc
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66765455"
---
# <a name="rollback-method-"></a>Método rollback ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Deshace todos los cambios realizados en la transacción actual y libera cualquier bloque en la base de datos que contenga en esos momentos este objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void rollback()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método rollBack es especificado por el método rollBack de la interfaz java.sql.Connection.  
  
 Este método se debería utilizar solamente cuando el modo de confirmación automática esté deshabilitado.  
  
## <a name="see-also"></a>Consulte también  
 [Método Rollback &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)   
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
