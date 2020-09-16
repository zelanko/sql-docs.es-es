---
description: Método finalize (SQLServerResultSet)
title: Método finalize (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.finalize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49bc879d-822b-42da-bc20-2394865f1f0f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f6f232e7755dd975edaa7b255e5ffe6dd9f85091
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437597"
---
# <a name="finalize-method-sqlserverresultset"></a>Método finalize (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cierra explícitamente este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>Observaciones  
 Cierra el conjunto de resultados si no lo hace la aplicación. Este método existe exclusivamente para ajustarse a las especificaciones de JDBC. Dado que la máquina virtual Java (JVM) no garantiza cuándo tendrá oportunidad de ejecutarse un finalizador, las aplicaciones que no cierren explícitamente sus conjuntos de resultados podrían seguir realizando interbloqueos en otra instrucción que utilice la misma conexión y esté bloqueada en un recurso de servidor común, como bloqueos de fila.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
