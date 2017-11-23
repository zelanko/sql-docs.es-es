---
title: "Método setObject (java.lang.String, java.lang.Object, int) | Documentos de Microsoft"
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
apiname: SQLServerCallableStatement.setObject (java.lang.String, java.lang.Object, int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: a9a0c802-7851-4826-b173-87b0c0acb3a0
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aa74e58019c49d1485026936eab9f9572ea4985f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setobject-method-javalangstring-javalangobject-int"></a>Método setObject (java.lang.String, java.lang.Object, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el valor del parámetro designado utilizando el tipo de objeto y de destino determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setObject(java.lang.String sCol,  
                      java.lang.Object o,  
                      int n)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
 *o*  
  
 Un **objeto** valor.  
  
 *n*  
  
 Un **int** que indica el tipo de destino, tal como se define en java.sql.Types.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setObject es especificado por el método setObject en la interfaz java.sql.CallableStatement.  
  
 A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0, el comportamiento de este método es modificado por la **sendTimeAsDatetime** propiedad de conexión ([estableciendo las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md)) y [ SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obtener más información, consulte [java.sql.Time cómo configurar los valores se envían al servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Método setObject &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
