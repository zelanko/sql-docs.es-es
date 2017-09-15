---
title: "setString (método) (SQLServerCallableStatement) | Documentos de Microsoft"
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
- SQLServerCallableStatement.setString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f38b97b5-d4f0-4f74-a33d-740241a85842
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2ebcac5fedd89cbec614d7278232c3a5e32e5740
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setstring-method-sqlservercallablestatement"></a>setString (método) (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado para el Java determinado **cadena** valor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setString(java.lang.String sCol,  
                      java.lang.String s)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
 *s*  
  
 A **cadena** valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setString es especificado por el método setString en la interfaz java.sql.CallableStatement.  
  
 Cadena a las conversiones binarias se llevan a cabo sólo cuando [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sabe el tipo de destino es binario. En casos donde el controlador JDBC no conoce el tipo subyacente, pasará el **cadena** literal y devolverá un error de servidor si el servidor no puede realizar la conversión.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
