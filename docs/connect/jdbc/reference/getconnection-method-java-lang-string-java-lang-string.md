---
title: getConnection Method (java.lang.String, java.lang.String) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fb33640c75d98fa065c6388458aaffc3067c3126
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 *Nombre de usuario*  
  
 A **cadena** que contiene el nombre de usuario.  
  
 *password*  
  
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
 [Método getConnection &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
