---
title: "Método getDouble (java.lang.String) | Documentos de Microsoft"
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
- SQLServerCallableStatement.getDouble (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8eab6a8e-91f3-47b1-8707-5e57368ad0c6
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4ce02952597f73f80ebb63f25314c1e88879171b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getdouble-method-javalangstring"></a>Método getDouble (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un **doble** en el lenguaje de según el nombre del parámetro de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public double getDouble(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 A **doble** valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getDouble es especificado por el método getDouble en la interfaz java.sql.CallableStatement.  
  
 Este método devuelve todos los tipos de datos basado en números con Java **doble** fidelidad.  
  
## <a name="see-also"></a>Vea también  
 [Método getDouble &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  

