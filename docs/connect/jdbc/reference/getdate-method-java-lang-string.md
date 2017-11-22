---
title: "parámetro de método (java.lang.String) getDate | Documentos de Microsoft"
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
apiname: SQLServerCallableStatement.getDate (java.lang.String)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: a605bca6-d960-4756-ad14-0f42b313e60a
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b9c6f53ea34214a92c4b39f61549826d164a2832
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getdate-method-javalangstring"></a>Método getDate (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.sql.Date en el lenguaje de programación Java según el nombre de parámetro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Date getDate(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de fecha.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getDate es especificado por el método getDate en la interfaz java.sql.CallableStatement.  
  
 Este método devuelve una parte de fecha válida de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** o **smalldatetime** tipo de datos, con la parte de hora establecida en la hora de inicio de Java de 00:00 (medianoche).  
  
## <a name="see-also"></a>Vea también  
 [getDate (método) &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
