---
title: Método supportsPositionedUpdate (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsPositionedUpdate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f963fb70-377d-43f5-8d56-326591f6d3e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73c85e41df64757a77bc26ff0b1a9534fdbb5ffa
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969011"
---
# <a name="supportspositionedupdate-method-sqlserverdatabasemetadata"></a>Método supportsPositionedUpdate (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite instrucciones UPDATE posicionadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsPositionedUpdate()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsPositionedUpdate especifica este método supportsPositionedUpdate en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
