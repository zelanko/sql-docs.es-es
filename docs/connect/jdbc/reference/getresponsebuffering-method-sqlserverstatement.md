---
description: María getResponseBuffering (SQLServerStatement)
title: Método getResponseBuffering (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResponseBuffering()
apilocation:
- SQLServerStatement.getResponseBuffering()
apitype: Assembly
ms.assetid: a9a9ffdd-7ce3-4e0a-907c-34d6a54e6865
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 08411235fe8e571e9f3bdaf7220f2387d3a0b5c0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434797"
---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>María getResponseBuffering (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el modo de almacenamiento en búfer de respuesta para este objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto **String** que contiene un atributo **full** o **adaptive** en minúscula.  
  
## <a name="remarks"></a>Observaciones  
 El valor **adaptive** especifica que se almacenen en búfer los menos datos posibles cuando sea necesario.  
  
 El valor **full** se especifica mediante la lectura del resultado completo desde el servidor en el tiempo de ejecución.  
  
 El valor **adaptive** es el predeterminado en la versión 2.0 y 3.0 del controlador JDBC. El valor **full** era el valor predeterminado antes de la versión 2.0 del controlador JDBC.  
  
 Para más información sobre cómo utilizar el modo de almacenamiento en búfer de respuesta, vea [Empleo de almacenamiento en búfer adaptable](../../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método setResponseBuffering &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
