---
title: Método setLoginTimeout (SQLServerDataSource) | Documentos de Microsoft
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
- SQLServerDataSource.setLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4e317ea333c0b1a7b456096405160b302c1b644a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>Método setLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el número de segundos que esto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto esperará mientras intenta efectuar una conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *LoginTimeout*  
  
 Un **int** valor que representa el número de segundos de espera. Un valor cero indica que el tiempo de espera es el predeterminado del sistema, que está especificado inicialmente en 15 segundos.  
  
## <a name="remarks"></a>Comentarios  
 Este método setLoginTimeout especificado por el método setLoginTimeout en la interfaz javax.sql.DataSource.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
