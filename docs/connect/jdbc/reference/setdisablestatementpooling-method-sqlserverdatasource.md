---
title: "setDisableStatementPooling (método) (SQLServerDataSource) | Documentos de Microsoft"
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
ms.openlocfilehash: 7588e8fc59067a604c977f940f7f7a3e39d20d73
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2018
---
# <a name="setdisablestatementpooling-method-sqlserverdatasource"></a>setDisableStatementPooling (método) (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el valor de la **disableStatementPooling** propiedad de conexión. Si es false, permite la declaración de agrupación para usarse de acoplamiento con statementPoolingCacheSize valor > 0.  

## <a name="syntax"></a>Sintaxis  
  
```
public void setDisableStatementPooling(boolean disableStatementPooling);  
```  
  
#### <a name="parameters"></a>Parámetros  
 *disableStatementPooling*  
  
 El nuevo valor de la **disableStatementPooling** propiedad de conexión.  

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentarios  
 Este método está disponible desde la versión del controlador JDBC 6.4 y hacia delante.
 
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
