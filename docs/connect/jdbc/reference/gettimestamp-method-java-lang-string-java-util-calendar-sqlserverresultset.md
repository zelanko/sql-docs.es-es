---
title: Método getTimestamp (java.lang.String, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTimestamp (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 44474000-8951-49ee-93a5-c8cb879eaf55
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a7aa807dc1cbcbd027cd4a5c26b43509438c67ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66767408"
---
# <a name="gettimestamp-method-javalangstring-javautilcalendar-sqlserverresultset"></a>Método getTimestamp (java.lang.String, java.util.Calendar) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor de nombre de columna designado en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un objeto java.sql.Timestamp en el lenguaje de programación Java; para ello, usa un objeto Calendar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Timestamp getTimestamp(java.lang.String colName,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *colName*  
  
 Valor **String** que contiene el nombre de columna.  
  
 *cal*  
  
 Un objeto de calendario.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de la marca de tiempo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getTimestamp especifica este método getTimestamp en la interfaz java.sql.ResultSet.  
  
 Este método solamente devuelve valores de columnas datetime y smalldatetime de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [getTimestamp (método) &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
