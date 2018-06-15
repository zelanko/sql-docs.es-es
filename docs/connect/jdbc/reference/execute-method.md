---
title: Método Execute () | Documentos de Microsoft
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
- SQLServerPreparedStatement.execute ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fa96d0f8-101b-422f-a767-405be9a5f74f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 89f349e0d2e333f2276a3fb75ae96cac25cdab51
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32829080"
---
# <a name="execute-method-"></a>Método execute ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ejecuta la instrucción SQL en este [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) objeto, que puede ser cualquier tipo de instrucción SQL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean execute()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si la instrucción devuelve un conjunto de resultados. **false** si devuelve un recuento de actualización o ningún resultado.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método de ejecución especificado por el método execute en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Vea también  
 [ejecutar el método &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)   
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
