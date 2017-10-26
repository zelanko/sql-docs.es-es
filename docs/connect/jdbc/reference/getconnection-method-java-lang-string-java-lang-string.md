---
title: getConnection Method (java.lang.String, java.lang.String) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 39b7a3bb2896ff308fc58510443bd54c487c77f8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getconnection-method-javalangstring-javalangstring"></a>Método getConnection (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Intenta establecer una conexión con los datos de origen que este [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto se representa mediante el nombre de usuario y contraseña.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *nombre de usuario*  
  
 A **cadena** que contiene el nombre de usuario.  
  
 *contraseña*  
  
 A **cadena** que contiene la contraseña.  
  
## <a name="return-value"></a>Valor devuelto  
 A [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentarios  
 Este método getConnection es especificado por el método getConnection en la interfaz javax.sql.DataSource.  
  
 Al llamar a la getConnection método con un nombre de usuario o contraseña reemplazará las propiedades de nombre y la contraseña de usuario que se establecen en la clase SQLServerDataSource al inicializar el objeto SQLServerConnection. Por ejemplo, si el llamador ha llamado a [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) y [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) en el origen de datos y, a continuación, llamadas getConnection y proporciona un valor no nulo nombre de usuario o una contraseña no es null, el nombre de usuario y la contraseña se establecen setUser y a setPassword se reemplazará por el nombre de usuario y contraseña que se pasan en getConnection.  
  
> [!NOTE]  
>  El nombre de usuario y la contraseña que se establecen en la dirección URL mediante una llamada a la [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md) método no se cambiará en este caso.  
  
## <a name="see-also"></a>Vea también  
 [Método getConnection &#40; SQLServerDataSource &#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

