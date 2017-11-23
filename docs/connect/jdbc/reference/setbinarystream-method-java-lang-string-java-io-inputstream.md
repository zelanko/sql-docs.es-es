---
title: "Método para la secuencia de entrada setBinaryStream) | Documentos de Microsoft"
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
ms.assetid: 339c8277-2d08-4094-9fa9-26c8ad3e7348
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bcf626164844136b416642462aaaf9ab3c95ad6e
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setbinarystream-method-javalangstring-javaioinputstream"></a>Método setBinaryStream (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el flujo de entrada especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setBinaryStream(java.lang.String parameterName,  
                            java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
 *x*  
  
 Un objeto InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setBinaryStream especificado por el método setBinaryStream en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [setBinaryStream &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setbinarystream-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
