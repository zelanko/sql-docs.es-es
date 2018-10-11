---
title: Método getConnection (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getConnection (java.lang.String, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 78db89d6-a8a0-4116-8885-548e627220ed
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f72babc3375c0720807322520a9761cb49e05919
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47677473"
---
# <a name="getconnection-method-javalangstring-javalangstring"></a>Método getConnection (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Intenta establecer una conexión con el origen de datos que representa este objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) mediante el nombre de usuario y contraseña especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Connection getConnection(java.lang.String username,  
                                         java.lang.String password)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *username*  
  
 Objeto **String** que contiene el nombre del usuario.  
  
 *password*  
  
 Objeto **String** que contiene la contraseña.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Notas  
 Este método getConnection especificado por el método getConnection en la interfaz javax.sql.DataSource.  
  
 Una llamada a la getConnection método con un nombre de usuario distinto de null o una contraseña, reemplazará las propiedades de nombre y la contraseña de usuario que se establecen en la clase SQLServerDataSource al inicializar el objeto SQLServerConnection. Por ejemplo, si el autor de llamada ha llamado a [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) y a [setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md) en el origen de datos y, a continuación, llama a getConnection y proporciona un nombre de usuario o contraseña que no sean NULL, el nombre de usuario y contraseña que se hayan establecido con setUser y setPassword se reemplazarán con el nombre de usuario y la contraseña que se hayan pasado en getConnection.  
  
> [!NOTE]  
>  El nombre de usuario y la contraseña que se establecen dentro de la dirección URL mediante una llamada al método [setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md), en este caso, no se verán modificados.  
  
## <a name="see-also"></a>Ver también  
 [Método getConnection &#40;SQLServerDataSource&#41;](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)   
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
