---
title: "getServerPreparedStatementDiscardThreshold (método) (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6ab3592fdaa20290a163e88d2d4b9d057a2f55a2
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2018
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>getServerPreparedStatementDiscardThreshold (método) (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el valor de **serverPreparedStatementDiscardThreshold** propiedad de conexión. Esta configuración controla cuántas pendientes preparado descarte instrucción acciones (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecuta una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1 unprepare acciones se ejecutan inmediatamente en cierre la instrucción preparada. Si este valor se establece en > 1 estas llamadas se procesan por lotes juntos para evitar una sobrecarga de la llamada a sp_unprepare con demasiada frecuencia.

  
## <a name="syntax"></a>Sintaxis  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve el **int** valor de la **serverPreparedStatementDiscardThreshold** propiedad de conexión.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentarios  
 Este método está disponible desde la versión del controlador JDBC 6.4 y hacia delante.
 
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
