---
title: "Método getBytes (SQLServerCallableStatement) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.getBytes
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: b6e88cea-54b3-4d18-a9af-db54abf19f45
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d1006144e75fd3e7e4366a29b1235dcca893c895
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getbytes-method-sqlservercallablestatement"></a>Método getBytes (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como una matriz de bytes.  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|Nombre|Description|  
|----------|-----------------|  
|[getBytes (int)](../../../connect/jdbc/reference/getbytes-method-int.md)|Recupera el valor del parámetro designado como una matriz del valor de bytes según el índice de parámetro.|  
|[getBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string.md)|Recupera el valor del parámetro designado como una matriz del valor de bytes según el nombre de parámetro.|  
  
## <a name="remarks"></a>Comentarios  
 En una versión anterior de la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], podría utilizar SQLServerCallableStatement.getBytes para convertir valores entre las matrices de bytes y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de datos **fecha**, **tiempo**, **datetime2**, o **datetimeoffset**. Ahora, al usar este método con esos tipos de datos, se producirá una excepción que indica que no se admite la conversión.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
