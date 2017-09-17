---
title: "Finalize (método) (SQLServerResultSet) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerResultSet.finalize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49bc879d-822b-42da-bc20-2394865f1f0f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6762b75f40e3b1fdc0a309c67dea461b1dada974
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
