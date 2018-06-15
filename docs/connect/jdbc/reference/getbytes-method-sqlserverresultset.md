---
title: Método getBytes (SQLServerResultSet) | Documentos de Microsoft
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
- SQLServerResultSet.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d16a0aea-6144-4fcb-bcbc-5d7daa36d327
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 549d4b30b062591cee69d4a7c089bfb8efefcf79
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32833260"
---
# <a name="getbytes-method-sqlserverresultset"></a>Método getBytes (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **bytes** matriz en el lenguaje de programación Java.  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|Nombre|Description|  
|----------|-----------------|  
|[getBytes (int)](../../../connect/jdbc/reference/getbytes-method-int-sqlserverresultset.md)|Recupera el valor del índice de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **bytes** matriz en el lenguaje de programación Java.|  
|[getBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string-sqlserverresultset.md)|Recupera el valor del nombre de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **bytes** matriz en el lenguaje de programación Java.|  
  
## <a name="remarks"></a>Comentarios  
 En una versión anterior de la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], podía utilizar SQLServerResultSet.getBytes para convertir valores entre las matrices de bytes y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de datos **fecha**, **tiempo**,  **datetime2**, o **datetimeoffset**. Ahora, al usar este método con esos tipos de datos, se producirá una excepción que indica que no se admite la conversión.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
