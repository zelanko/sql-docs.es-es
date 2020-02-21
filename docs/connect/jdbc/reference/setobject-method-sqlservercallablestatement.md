---
title: Método setObject (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setObject
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7110f6c5-4af3-4b50-a4d4-1bae1876c70d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bdd1912a04c503b59064a0e39859a5845c4c6b0d
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67973301"
---
# <a name="setobject-method-sqlservercallablestatement"></a>Método setObject (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el valor del parámetro designado utilizando el objeto determinado.  
  
 Desde el controlador JDBC 3.0 de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el comportamiento de este método queda modificado por la propiedad de conexión **sendTimeAsDatetime** ([Establecimiento de las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md)) y [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para más información, vea [Configurar el modo en que los valores java.sql.Time se envían al servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|Nombre|Descripción|  
|----------|-----------------|  
|[setObject (java.lang.String, java.lang.Object)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object.md)|Establece el valor del parámetro designado utilizando el objeto determinado.|  
|[setObject (java.lang.String, java.lang.Object, int)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int.md)|Establece el valor del parámetro designado mediante el uso del objeto y tipo de destino determinados.|  
|[setObject (java.lang.String, java.lang.Object, int, int)](../../../connect/jdbc/reference/setobject-method-java-lang-string-java-lang-object-int-int.md)|Establece el valor del parámetro designado mediante el uso del objeto, tipo de destino y escala determinados.|  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
