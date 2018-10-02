---
title: Método getUser (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3513dd7f-6ae5-4010-bde0-454ac4365bce
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34d7c710372114d9c11d9a4f8278fa041482f0bf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47597170"
---
# <a name="getuser-method-sqlserverdatasource"></a>Método getUser (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el nombre de usuario que se utiliza para la conexión al origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getUser()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto **String** que contiene el nombre del usuario.  
  
## <a name="remarks"></a>Notas  
 El método [setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md) establece el nombre de usuario que se utilizará al conectar a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si no se establece un valor de nombre de usuario, el método getUser devuelve el valor predeterminado o NULL.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
