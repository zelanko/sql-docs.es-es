---
title: "Método getXAConnection () | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerXADataSource.getXAConnection ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b2710613-78b1-438f-b996-c7ae6f34381a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6fd5681b0ece55e113d03c9ee21950f1cae19f43
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getxaconnection-method-"></a>Método getXAConnection ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Intenta establecer una conexión a una base de datos física que se puede utilizar en una transacción distribuida.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public javax.sql.XAConnection getXAConnection()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto XAConnection.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentarios  
 Este método getXAConnection especificado por el método getXAConnection en la interfaz javax.sql.XADataSource.  
  
> [!NOTE]  
>  Las implementaciones del grupo de conexiones XA, y no los códigos de aplicación JDBC, llaman normalmente a este método.  
  
## <a name="see-also"></a>Vea también  
 [Método getXAConnection &#40; SQLServerXADataSource &#41;](../../../connect/jdbc/reference/getxaconnection-method-sqlserverxadatasource.md)   
 [Métodos SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [Miembros de SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [Clase SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
