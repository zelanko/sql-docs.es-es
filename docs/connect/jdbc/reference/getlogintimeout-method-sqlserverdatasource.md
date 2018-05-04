---
title: Método getLoginTimeout (SQLServerDataSource) | Documentos de Microsoft
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
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dcaccc8a16561f43b4ada72d1e07bad291b6ec2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>Método getLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el número de segundos que este [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto esperará mientras intenta efectuar una conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** valor que representa el número de segundos de espera.  
  
## <a name="remarks"></a>Comentarios  
 Si la aplicación no especifica un valor de tiempo de forma explícita, este método devuelve un valor predeterminado de 15 segundos.  
  
 Este método getLoginTimeout especificado por el método getLoginTimeout en la interfaz javax.sql.DataSource.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
