---
title: "Método getFloat (java.lang.String) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.getFloat (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: b6492341-fdc2-449c-9d03-95a5dadf1bb0
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 208bba07d833dbdbb80bd88d8e9cd5aeee1a2a46
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getfloat-method-javalangstring"></a>Método getFloat (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un **float** en el lenguaje de según el nombre del parámetro de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public float getFloat(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 A **float** valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getFloat es especificado por el método getFloat en la interfaz java.sql.CallableStatement.  
  
 Este método devuelve todos los tipos de número con Java **float** fidelidad.  
  
## <a name="see-also"></a>Vea también  
 [Método getFloat &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getfloat-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
