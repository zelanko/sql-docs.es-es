---
title: getDateTimeOffset(java.lang.string) (SQLServerResultSet) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e585927c-0dee-43fd-b71e-c9f1701790bd
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26baa74f60cf04c712d6e8c6a0addec057893109
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getdatetimeoffsetjavalangstring-sqlserverresultset"></a>getDateTimeOffset(java.lang.string) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Este método se agregó en [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0.  
  
 Recupera el valor de la columna designada como un [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) objeto en el lenguaje según el índice de parámetro de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(String columnName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 Nombre de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 A [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Puede actualizar una [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) valor con [SQLServerResultSet.updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md).  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

