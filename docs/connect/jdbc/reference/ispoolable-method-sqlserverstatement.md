---
description: Método isPoolable (SQLServerStatement)
title: Método isPoolable (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8a12ac5-57cb-4288-9973-c7d5cebd197c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1b8b3e817ddaf2983d1cfec64099c220e012e16
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433487"
---
# <a name="ispoolable-method-sqlserverstatement"></a>Método isPoolable (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un valor que indica si una instrucción se puede agregar al grupo de instrucciones proporcionado por el usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isPoolable() throws SQLException  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si la instrucción se puede agregar al grupo de instrucciones que proporciona el usuario. En caso contrario, es **false**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 [setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md) cambia el comportamiento agrupable de un objeto.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
