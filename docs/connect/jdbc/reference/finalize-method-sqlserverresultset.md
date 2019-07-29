---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7afb8728b92ac7460173950bf42e38f968e056af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954564"
---
# <a name="finalize-method-sqlserverresultset"></a>Método finalize (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cierra explícitamente este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>Notas  
 Cierra el conjunto de resultados si no lo hace la aplicación. Este método existe exclusivamente para ajustarse a las especificaciones de JDBC. Dado que la máquina virtual Java (JVM) no garantiza cuándo tendrá oportunidad de ejecutarse un finalizador, las aplicaciones que no cierren explícitamente sus conjuntos de resultados podrían seguir realizando interbloqueos en otra instrucción que utilice la misma conexión y esté bloqueada en un recurso de servidor común, como bloqueos de fila.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
