---
title: Método getMoreResults () | Documentos de Microsoft
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
- SQLServerStatement.getMoreResults ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: df89db50-0b2f-4094-820a-30be25ad72fe
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2c39a59f723cf24932b70bac44074c3ad8c4b82
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32836110"
---
# <a name="getmoreresults-method-"></a>Método getMoreResults ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Se desplaza al próximo resultado de esto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final boolean getMoreResults()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si el resultado devuelto es un conjunto de resultados. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getMoreResults especificado por el método getMoreResults en la interfaz java.sql.Statement.  
  
 Llamar al método getMoreResults implícitamente cierra los objetos de conjunto de resultados abiertos actualmente que se obtienen con el [getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) método.  
  
## <a name="see-also"></a>Vea también  
 [Método getMoreResults &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
