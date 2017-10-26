---
title: "Método getFetchDirection (SQLServerStatement) | Documentos de Microsoft"
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
- SQLServerStatement.getFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ceb4ae68-decc-46d3-83f1-0bbd23aaf58c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ae039ccdc76cdc6117f502971feafe683f58b0d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getfetchdirection-method-sqlserverstatement"></a>Método getFetchDirection (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera la dirección para capturar las filas de tablas de base de datos que es el valor predeterminado de conjuntos de resultados que se generan a partir de esto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.  
  
> [!NOTE]  
>  Este método no se implementa actualmente por la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Por consiguiente, siempre devolverá FETCH_UNKNOWN.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final int getFetchDirection()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica la dirección de la captura que se especifica mediante la [setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md) método.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getFetchDirection especificado por el método getFetchDirection en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

