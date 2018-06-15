---
title: updateDateTimeOffset(string) (SQLServerResultSet) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 952947ce-7c6e-4364-b035-46cb7fe621b2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf422903a4c03258a7c3fc9a4d42f6525ababd9b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32850400"
---
# <a name="updatedatetimeoffsetstring-microsoftsqldatetimeoffset-sqlserverresultset"></a>updateDateTimeOffset(string, microsoft.sql.DateTimeOffset) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Este método se agregó en [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0.  
  
 Actualiza el valor de la columna especificada en el [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) valor, dado un nombre de columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 El nombre de una columna.  
  
 *x*  
  
 A [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Puede recuperar un [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) valor con [SQLServerResultSet.getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md).  
  
## <a name="see-also"></a>Vea también  
 [updateDateTimeOffset &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
