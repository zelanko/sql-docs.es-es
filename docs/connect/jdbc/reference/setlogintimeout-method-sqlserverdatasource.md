---
title: "Método setLoginTimeout (SQLServerDataSource) | Documentos de Microsoft"
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
apiname: SQLServerDataSource.setLoginTimeout
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: b63d1cf4-dc1b-4e35-9a56-50436642eaaf
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4a65f835792fc342cbbcc3803c9a3be6d0bb9214
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setlogintimeout-method-sqlserverdatasource"></a>Método setLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el número de segundos que esto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto esperará mientras intenta efectuar una conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setLoginTimeout(int loginTimeout)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *loginTimeout*  
  
 Un **int** valor que representa el número de segundos de espera. Un valor cero indica que el tiempo de espera es el predeterminado del sistema, que está especificado inicialmente en 15 segundos.  
  
## <a name="remarks"></a>Comentarios  
 Este método setLoginTimeout especificado por el método setLoginTimeout en la interfaz javax.sql.DataSource.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
