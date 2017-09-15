---
title: "Método updateObject (java.lang.String, java.lang.Object, int) | Documentos de Microsoft"
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
- SQLServerResultSet.updateObject (java.lang.String, java.lang.Object, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 27283ce1-637e-4e2c-91ee-8ad379114ac5
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 89ac0f91994687dfc94ed5175b73912dbf276f45
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="updateobject-method-javalangstring-javalangobject-int"></a>Método updateObject (java.lang.String, java.lang.Object, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un **objeto** valor según el nombre de columna y la escala.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateObject(java.lang.String columnName,  
                         java.lang.Object x,  
                         int scale)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 A **cadena** que contiene el nombre de columna.  
  
 *obj*  
  
 Un **objeto** valor.  
  
 *escala*  
  
 Para tipos java.sql.Types.NUMERIC o java.sql.Types.DECIMAL, este es el número de dígitos tras el separador decimal. Para todos los demás tipos se omite este valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateObject es especificado por el método updateObject en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Vea también  
 [Método updateObject &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
