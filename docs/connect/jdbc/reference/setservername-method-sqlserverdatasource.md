---
title: Método setServerName (SQLServerDataSource) | Documentos de Microsoft
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
- SQLServerDataSource.setServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70920828-eda0-4064-be9f-c1e460db8f00
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8843d601229fc8db7e374857857841eb5e3fc52a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32844810"
---
# <a name="setservername-method-sqlserverdatasource"></a>Método setServerName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el nombre del equipo que está ejecutando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setServerName(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ServerName*  
  
 A **cadena** que contiene el nombre del servidor.  
  
## <a name="remarks"></a>Comentarios  
 El nombre del servidor es el nombre de host del equipo de destino que se está ejecutando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Si no se establece la propiedad serverName, [getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md) devuelve el valor predeterminado es null.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
