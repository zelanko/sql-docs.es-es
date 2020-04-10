---
title: Método getWarnings (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getWarnings
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 15af39bf-6285-44cc-a021-7341e7a055c4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de587ef505a1314e543f794431ee977e55ee3ab3
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80910391"
---
# <a name="getwarnings-method-sqlserverconnection"></a>Método getWarnings (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la primera advertencia que notifican las llamadas en este objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.SQLWarning getWarnings()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto SQLWarning.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getWarnings especifica este método getWarnings en la interfaz java.sql.Connection.  
  
 Las advertencias posteriores se encadenan al primer método SQLWarning y se llaman con el método getNextWarning. Si se llama en una conexión cerrada, se producirá una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
