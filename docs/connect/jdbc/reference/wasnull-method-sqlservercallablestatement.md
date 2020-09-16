---
description: Método wasNull (SQLServerCallableStatement)
title: Método wasNull (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.wasNull
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1a27b2fe-ae12-46a9-9bca-2c5ca66b9eb3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e006643abaadc42c5c8f5f7c0b16d6cf2ecf9648
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488025"
---
# <a name="wasnull-method-sqlservercallablestatement"></a>Método wasNull (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si la última lectura del parámetro OUT incorporaba el valor de NULL de SQL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean wasNull()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si la última lectura de parámetro fue NULL. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método wasNull lo especifica el método wasNull en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
