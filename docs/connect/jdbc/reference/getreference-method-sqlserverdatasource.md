---
title: Método getReference (SQLServerDataSource) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getReference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b3fb1a97-86ee-4977-adca-c35ae199dbb3
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b35f7ea76e51327bd6e4605fad28aa5f29e79b16
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getreference-method-sqlserverdatasource"></a>Método getReference (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve una referencia a este [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public javax.naming.Reference getReference()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de referencia.  
  
## <a name="remarks"></a>Comentarios  
 Este método getReference especificado por el getReference (método) en la interfaz javax.naming.Referenceable.  
  
 Anteriores a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0, si se llamaba a sqlserverdatasource.settruststorepassword en un objeto SQLServerDataSource, la contraseña estará presente en el objeto devuelto por SQLServerDataSource.getReference, lo que el objeto que se usará para realizar conexiones adicionales. Con el controlador JDBC 3.0, se necesitará establecer la contraseña en el objeto que devuelve SQLServerDataSource.getReference antes de realizar las conexiones con el objeto.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
