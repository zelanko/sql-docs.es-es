---
description: Método jdbcCompliant (SQLServerDriver)
title: Método jdbcCompliant (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.jdbcCompliant
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b299b20d-d1cd-45b3-91dc-dcf579498570
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25495005dafdc95982b2f7005c96eb186c864caf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433287"
---
# <a name="jdbccompliant-method-sqlserverdriver"></a>Método jdbcCompliant (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Comprueba que [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] es conforme a la especificación JDBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean jdbcCompliant()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si el controlador JDBC cumple los requisitos mínimos. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Observaciones  
 El método jdbcCompliant especifica este método jdbcCompliant en la interfaz java.sql.Driver.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Miembros de SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Clase SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
