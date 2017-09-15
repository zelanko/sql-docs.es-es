---
title: "setBytes (método) (SQLServerPreparedStatement) | Documentos de Microsoft"
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
- SQLServerPreparedStatement.setBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 52e99ef9-b786-4a14-bfc5-4162e46aafbb
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 909e36d5eb80b2642c7d68fff7d28c625045c283
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setbytes-method-sqlserverpreparedstatement"></a>setBytes (método) (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en la matriz de bytes determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setBytes(int n,  
                           byte[] x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *n*  
  
 Un **int** que indica el número de parámetro.  
  
 *x*  
  
 Matriz de bytes.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setBytes es especificado por el método setBytes en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
