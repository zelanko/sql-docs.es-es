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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef07d4a60e3d32faaaabee923c1c23a79ce8b91a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928096"
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
  
  
