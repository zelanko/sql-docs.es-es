---
description: Método supportsMixedCaseIdentifiers (SQLServerDatabaseMetaData)
title: Método supportsMixedCaseIdentifiers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsMixedCaseIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0f68d9f7-0d8d-4d8d-9188-14e253a2576a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25aecc12f5e8a8e9d02401afae4d9830a71f6f0e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467001"
---
# <a name="supportsmixedcaseidentifiers-method-sqlserverdatabasemetadata"></a>Método supportsMixedCaseIdentifiers (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos trata a los identificadores de SQL con combinaciones de mayúsculas y minúsculas que no se entrecomillan como elementos que distinguen entre mayúsculas y minúsculas y los almacena combinando ambos formatos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsMixedCaseIdentifiers()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si los identificadores están almacenados combinando mayúsculas y minúsculas. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsMixedCaseIdentifiers especifica este método supportsMixedCaseIdentifiers en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
