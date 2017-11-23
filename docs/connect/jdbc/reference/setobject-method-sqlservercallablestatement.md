---
title: "Método setObject (SQLServerCallableStatement) | Documentos de Microsoft"
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
apiname: SQLServerCallableStatement.setObject
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 7110f6c5-4af3-4b50-a4d4-1bae1876c70d
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 77f3add6ad521d097dccc09a801db3acf9bb37a3
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setobject-method-sqlservercallablestatement"></a>Método setObject (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el valor del parámetro designado utilizando el objeto especificado.  
  
 A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0, el comportamiento de este método es modificado por la **sendTimeAsDatetime** propiedad de conexión ([estableciendo las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md)) y [ SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obtener más información, consulte [java.sql.Time cómo configurar los valores se envían al servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|Nombre|Description|  
|----------|-----------------|  
|[setObject (java.lang.String, java.lang.Object)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object.md)|Establece el valor del parámetro designado utilizando el objeto especificado.|  
|[setObject (java.lang.String, java.lang.Object, int)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int.md)|Establece el valor del parámetro designado mediante el uso del objeto y tipo de destino determinados.|  
|[setObject (java.lang.String, java.lang.Object, int, int)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int-int.md)|Establece el valor del parámetro designado mediante el uso del objeto, tipo de destino y escala determinados.|  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
