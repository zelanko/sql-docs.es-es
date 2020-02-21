---
title: Método getReference (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3fb1a97-86ee-4977-adca-c35ae199dbb3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c4774dcda174d5260289409053a892cc4039b4f0
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67980462"
---
# <a name="getreference-method-sqlserverdatasource"></a>Método getReference (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve una referencia a este objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Reference.  
  
## <a name="remarks"></a>Observaciones  
 El método getReference especifica este método getReference en la interfaz javax.naming.Referenceable.  
  
 Antes del controlador JDBC 3.0 de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], si se llamaba a SQLServerDataSource.setTrustStorePassword en un objeto SQLServerDataSource, la contraseña aparecería en el objeto que devuelve SQLServerDataSource.getReference, lo cual haría posible utilizar el objeto para realizar conexiones adicionales. Con el controlador JDBC 3.0, se necesitará establecer la contraseña en el objeto que devuelve SQLServerDataSource.getReference antes de realizar las conexiones con el objeto.  
  
 También, si establece SQLServerDataSource.setTrustStorePassword antes de enlazar las propiedades de origen de datos, deberá llamar a SQLServerDataSource.setTrustStorePassword antes de obtener la conexión. Por ejemplo,  
  
```  
ctx = new InitialContext(System.getProperties());  
  
SQLServerDataSource ds1 = (SQLServerDataSource) ctx.lookup(jndiName);  
  
ds1.setTrustStorePassword("XXXXX");  
Connection con = ds1.getConnection("user", "XXXXXX");  
  
ctx.rebind(jndiName, ds1);  
SQLServerDataSource ds2 = (SQLServerDataSource) ctx.lookup(jndiName);  
ds2.setTrustStorePassword("XXXXX");   // reset the truststore password  
con = ds2.getConnection("user", "XXXXXX");   // provide userid and password again  
```  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
