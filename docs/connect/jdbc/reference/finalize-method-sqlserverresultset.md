---
title: Finalize (método) (SQLServerResultSet) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.finalize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49bc879d-822b-42da-bc20-2394865f1f0f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 56c7131bfc0b5f1bb293b7a697f090495f0938f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32827480"
---
# <a name="finalize-method-sqlserverresultset"></a>Finalize (método) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Esto cierra explícitamente [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>Comentarios  
 Cierra el conjunto de resultados si no lo hace la aplicación. Este método existe exclusivamente para ajustarse a las especificaciones de JDBC. Dado que la máquina virtual Java (JVM) no garantiza cuándo tendrá oportunidad de ejecutarse un finalizador, las aplicaciones que no cierren explícitamente sus conjuntos de resultados podrían seguir realizando interbloqueos en otra instrucción que utilice la misma conexión y esté bloqueada en un recurso de servidor común, como bloqueos de fila.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
