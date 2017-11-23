---
title: "Método getUser (SQLServerDataSource) | Documentos de Microsoft"
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
apiname: SQLServerDataSource.getUser
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 3513dd7f-6ae5-4010-bde0-454ac4365bce
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d0be6cc3ac11282b6188129a6b04f3f47043862b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getuser-method-sqlserverdatasource"></a>Método getUser (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el nombre de usuario que se utiliza para la conexión al origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getUser()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** que contiene el nombre de usuario.  
  
## <a name="remarks"></a>Comentarios  
 El [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) método establece el nombre de usuario que se utilizará al conectarse a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Si no se establece un valor de nombre de usuario, el método getUser devuelve el valor predeterminado o NULL.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
