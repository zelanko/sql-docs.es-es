---
title: Método setServerName (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70920828-eda0-4064-be9f-c1e460db8f00
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a3c099e8bd441ee263202499036e25c738c9898f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66767975"
---
# <a name="setservername-method-sqlserverdatasource"></a>Método setServerName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el nombre del equipo que ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setServerName(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *serverName*  
  
 Objeto **String** que contiene el nombre del servidor.  
  
## <a name="remarks"></a>Notas  
 El nombre del servidor es el nombre de host del equipo de destino que ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si no se establece la propiedad serverName, [getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md) devuelve el valor predeterminado, que es NULL.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
