---
title: supportsResultSetHoldability método (SQLServerDatabaseMetaData) | Documentos de Microsoft
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
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.supportsResultSetHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ab575792-fd11-4ff3-8847-1368e7a322c5
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb4630dd266aef728c02696c0616b1c3c62cf5c3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="supportsresultsetholdability-method-sqlserverdatabasemetadata"></a>supportsResultSetHoldability Método (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite la capacidad de alojamiento del conjunto de resultados determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsResultSetHoldability(int holdability)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *capacidad de alojamiento*  
  
 Un **int** que indica el conjunto de resultados capacidad de alojamiento, que puede ser uno de los siguientes valores:  
  
 ResultSet.HOLD_CURSORS_OVER_COMMIT  
  
 ResultSet.CLOSE_CURSORS_AT_COMMIT  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si se admite. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método supportsResultSetHoldability especificado por el método supportsResultSetHoldability en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
