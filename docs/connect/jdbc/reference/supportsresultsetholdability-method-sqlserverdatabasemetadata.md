---
description: supportsResultSetHoldability Método (SQLServerDatabaseMetaData)
title: Método supportsResultSetHoldability (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsResultSetHoldability
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ab575792-fd11-4ff3-8847-1368e7a322c5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d0ed1388fd8e3d137fbaae9d7bc8b66235a8a5fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354001"
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
  
 Un valor **int** que indica la capacidad de alojamiento del conjunto de resultados, que puede ser uno de los siguientes valores:  
  
 ResultSet.HOLD_CURSORS_OVER_COMMIT  
  
 ResultSet.CLOSE_CURSORS_AT_COMMIT  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsResultSetHoldability especifica este método supportsResultSetHoldability en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
