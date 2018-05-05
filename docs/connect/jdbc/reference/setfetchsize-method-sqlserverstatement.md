---
title: Método setFetchSize (SQLServerStatement) | Documentos de Microsoft
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
- SQLServerStatement.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 760e555e-9667-4b40-b0ba-778026ff2923
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6543890d57f38da792ba3b8657750a22fb09012e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setfetchsize-method-sqlserverstatement"></a>Método setFetchSize (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Proporciona el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] una sugerencia sobre el número de filas que se deben capturar en la base de datos cuando se necesitan más filas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Filas*  
  
 Un **int** que indica el número de filas que se va a capturar.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setFetchSize especificado por el método setFetchSize en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
