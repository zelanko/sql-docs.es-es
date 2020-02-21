---
title: Método setObject (java.lang.String, java.lang.Object) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setObject (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 14b84409-5510-4642-a83b-732d8511c5b1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d07f5026ccc4ee5a614f1f3fa5020502f9dcadd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67973320"
---
# <a name="setobject-method-javalangstring-javalangobject"></a>Método setObject (java.lang.String, java.lang.Object)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el valor del parámetro designado utilizando el objeto determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setObject(java.lang.String sCol,  
                      java.lang.Object o)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *o*  
  
 Valor **Object**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setObject especifica este método setObject en la interfaz java.sql.CallableStatement.  
  
 Este método convierte el parámetro especificado en un tipo de datos CHAR si se especifica un valor NULL, antes de enviarlo a la base de datos. Si el parámetro se declara como un tipo de SQL binary, varbinary o image, se producirá una excepción cuando se ejecute la instrucción.  
  
 Desde el controlador JDBC 3.0 de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el comportamiento de este método queda modificado por la propiedad de conexión **sendTimeAsDatetime** ([Establecimiento de las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md)) y [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para más información, vea [Configurar el modo en que los valores java.sql.Time se envían al servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método setObject &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
