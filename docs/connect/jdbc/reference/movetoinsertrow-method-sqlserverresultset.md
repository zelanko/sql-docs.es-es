---
title: moveToInsertRow (método) (SQLServerResultSet) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerResultSet.moveToInsertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3c54bfe-d5b7-4f6e-ae6c-3e8954e5b1c9
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f39608188e9de998c5f431561cf1482f5d50b3f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="movetoinsertrow-method-sqlserverresultset"></a>moveToInsertRow (método) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Mueve el cursor a la fila de inserción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void moveToInsertRow()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método moveToInsertRow especificado por el método moveToInsertRow en la interfaz java.sql.ResultSet.  
  
 Se recuerda la posición del cursor actual mientras el cursor se coloca en la fila de inserción. La fila de inserción es una fila especial que está asociada a un conjunto de resultados con capacidad de actualización. Se trata básicamente de un búfer donde se puede generar una nueva fila si se llama a los métodos updater antes de agregar la fila al conjunto de resultados.  
  
 Solo el actualizador, captador y [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) se puede llamar a métodos cuando el cursor está en la fila de inserción. Todas las columnas de un conjunto de resultados debe proporcionar un valor cada vez que se llama a este método y antes de llamar a insertRow. Se debe llamar a un método updater antes de poder llamar a un método getter en un valor de columna.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
