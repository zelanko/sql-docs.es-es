---
title: "Método setTimestamp al valor de marca de tiempo | Documentos de Microsoft"
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
apiname: SQLServerCallableStatement.setTimestamp (java.lang.String, java.sql.Timestamp)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: dc45b126-3196-47ff-956b-cbc897980ff8
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 96d2cac5175dbe4dfc63e96afd1cb8676e750dff
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="settimestamp-method-javalangstring-javasqltimestamp"></a>Método setTimestamp (java.lang.String, java.sql.Timestamp)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado para el valor de marca de tiempo determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setTimestamp(java.lang.String sCol,  
                         java.sql.Timestamp t)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
 *t*  
  
 Un objeto de la marca de tiempo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setTimestamp especificado por el método setTimestamp en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [Método setTimestamp &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/settimestamp-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
