---
title: Método getObject (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getObject (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a1e955ce-13db-4828-ad59-d9b6a8b2c6cc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 56fc766c22751ea0a1465f9d1a447653b096b8f8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66787465"
---
# <a name="getobject-method-javalangstring"></a>Método getObject (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto en el lenguaje de programación Java según el nombre del parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.Object getObject(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Valor **Object**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getObject especifica este método getObject en la interfaz java.sql.CallableStatement.  
  
 Este método devolverá el valor de la columna determinada como un objeto de Java. El tipo del objeto de Java será el tipo de objeto de Java predeterminado que corresponde al tipo SQL de la columna, tras la asignación para los tipos integrados que se indica en las especificaciones de JDBC. Si el valor es NULL de SQL, el controlador devuelve un NULL de Java.  
  
 Este método también se puede utilizar para leer los tipos de datos abstractos específicos de la base de datos. En la API de JDBC 2.0, el comportamiento del método getObject se extiende para materializar datos de tipos de SQL definidos por el usuario. Cuando una columna contiene un valor estructurado o distinto, el comportamiento de este método es como si se llamara a `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())`.  
  
 A partir del controlador JDBC 3.0 de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Se devolverá un valor de tipo **date** como un objeto java.sql.Date.  
  
-   Se devolverá un valor de tipo **time** como un objeto java.sql.Time.  
  
-   Se devolverá un valor de tipo **datetime2** como un objeto java.sql.Timestamp.  
  
-   Se devolverá un valor de tipo **datetimeoffset** como un objeto microsoft.sql.DateTimeOffset.  
  
## <a name="see-also"></a>Consulte también  
 [Método getObject &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
