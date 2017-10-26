---
title: "Cancel (método) (SQLServerStatement) | Documentos de Microsoft"
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
- SQLServerStatement.cancel
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 276bd9c1-9329-4fc9-9622-ed673c83a12d
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b906ee23d28e42ff105d5d9bb919453193d90f68
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="cancel-method-sqlserverstatement"></a>Método cancel (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cancela la instrucción SQL que se esté ejecutando este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void cancel()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método de cancelación especificado por el método de cancelación en la interfaz java.sql.Statement.  
  
 Cuando se ejecuta una instrucción que genera un conjunto de resultados grande de solo avance y solo lectura, es posible que únicamente esté interesado en algún conjunto inicial de filas en el conjunto de resultados que se ha devuelto. En este caso, la aplicación puede llamar a la [cancelar](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) establece método de objeto de instrucción asociado antes de cerrar el resultado con el fin de minimizar el tiempo de procesamiento necesario para descartar las filas innecesarias restantes. Recomendamos comparar los inconvenientes entre el tiempo de procesamiento que se ahorraría y el tiempo y el viaje de ida y vuelta al servidor que se necesita para cancelar la ejecución a la hora de decidir si utilizar o no esta técnica.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  

