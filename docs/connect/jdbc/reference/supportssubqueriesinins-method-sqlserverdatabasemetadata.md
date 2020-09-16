---
description: Método supportsSubqueriesInIns (SQLServerDatabaseMetaData)
title: Método supportsSubqueriesInIns (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsSubqueriesInIns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 77a0b5c0-0d8e-4e08-975f-4eeabb108ab1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 21cafb0fc227285c933ecb852ee4588b5ab43f29
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450137"
---
# <a name="supportssubqueriesinins-method-sqlserverdatabasemetadata"></a>Método supportsSubqueriesInIns (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite subconsultas en instrucciones IN.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsSubqueriesInIns()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsSubqueriesInIns especifica este método supportsSubqueriesInIns en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
