---
title: Método updateBytes (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3050c836-fbb3-4475-99e5-05637a48a932
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c58b9198e3e5472a27b37ab36f4a7747c33eef12
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755150"
---
# <a name="updatebytes-method-sqlserverresultset"></a>Método updateBytes (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con una matriz de valores **byte**.  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|Nombre|Descripción|  
|----------|-----------------|  
|[updateBytes (int, byte&#91;&#93;)](../../../connect/jdbc/reference/updatebytes-method-int-byte.md)|Actualiza la columna designada con una matriz de valores **byte** según el índice de columna.|  
|[updateBytes (java.lang.String, byte&#91;&#93;)](../../../connect/jdbc/reference/updatebytes-method-java-lang-string-byte.md)|Actualiza la columna designada con una matriz de valores **byte** según el nombre de columna.|  
  
## <a name="remarks"></a>Notas  
 En una versión anterior de [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)], se podía usar SQLServerResultSet.updateBytes para convertir valores entre matrices de bytes y tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **date**, **time**, **datetime2** o **datetimeoffset**. Ahora, al usar este método con esos tipos de datos, se producirá una excepción que indica que no se admite la conversión.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
