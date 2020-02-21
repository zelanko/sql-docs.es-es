---
title: Método getDriverVersion (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getDriverVersion
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3be84d65-af61-4c34-b052-74a5d488eaa9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd67749bc8dcb29617c97a441c9858b3bb8fb6f5
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67983420"
---
# <a name="getdriverversion-method-sqlserverdatabasemetadata"></a>Método getDriverVersion (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número de versión de este controlador JDBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getDriverVersion()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **String** que contiene la versión del controlador JDBC.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getDriverVersion especifica este método getDriverVersion en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
