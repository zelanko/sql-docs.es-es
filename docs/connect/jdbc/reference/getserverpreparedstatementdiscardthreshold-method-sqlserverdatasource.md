---
title: Método getServerPreparedStatementDiscardThreshold (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 13c2512b3d66a324947c73c7d5030c03a1e9294e
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66791885"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource"></a>Método getServerPreparedStatementDiscardThreshold (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el valor de **valor de serverPreparedStatementDiscardThreshold** propiedad de conexión. Esta configuración controla cuántos pendientes preparado descarte instrucción acciones (sp_unprepare) pueden estar pendientes por conexión antes de que se ejecuta una llamada para limpiar los controladores pendientes en el servidor. Si el valor es < = 1 unprepare acciones se ejecutan inmediatamente en la instrucción preparada cierre. Si este valor se establece en 1 > estas llamadas se procesan por lotes juntos para evitar una sobrecarga de la llamada a sp_unprepare con demasiada frecuencia.

  
## <a name="syntax"></a>Sintaxis  
  
```
public int getServerPreparedStatementDiscardThreshold();  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve el **int** valor de la **valor de serverPreparedStatementDiscardThreshold** propiedad de conexión.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Notas  
 Este método está disponible desde la versión del controlador JDBC 6.4 y en marcha.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
