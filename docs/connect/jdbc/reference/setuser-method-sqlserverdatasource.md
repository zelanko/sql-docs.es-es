---
title: Método setUser (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setUser
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d2ea7906-2d10-438d-aa51-f576eea923c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f3953763dc1b8a0d24e4c335b5b465c49707174
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47784163"
---
# <a name="setuser-method-sqlserverdatasource"></a>Método setUser (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el nombre de usuario que se utiliza para la conexión al origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setUser(java.lang.String user)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *user*  
  
 Objeto **String** que contiene el nombre del usuario.  
  
## <a name="remarks"></a>Notas  
 El método setUser establece el nombre de usuario que se utilizará para conectar a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si no se establece un valor de nombre de usuario, el método [getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md) devuelve el valor predeterminado o NULL.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
