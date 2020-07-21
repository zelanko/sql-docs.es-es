---
title: Método getTime (java.lang.String, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getTime (java.lang.String, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 13b51f77-cec9-45fc-862e-3d2bb2d718d7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ae0c60471595aebeee08a2ad949c0170371f8cf
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927425"
---
# <a name="gettime-method-javalangstring-javautilcalendar-sqlserverresultset"></a>Método getTime (java.lang.String, java.util.Calendar) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del nombre de columna designado en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un objeto java.sql.Time en el lenguaje de programación Java; para ello, usa el objeto Calendar determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Time getTime(java.lang.String colName,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *colName*  
  
 Valor **String** que contiene el nombre de columna.  
  
 *cal*  
  
 Un objeto Calendar.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Time.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getTime especifica este método getTime en la interfaz java.sql.ResultSet.  
  
 Este método devuelve una hora válida que forma parte de un tipo de datos datetime o smalldatetime de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], con la parte correspondiente a la fecha establecida en la fecha de inicio de Java de 1970/01/01 en la zona horaria del calendario suministrado.  
  
## <a name="see-also"></a>Consulte también  
 [Método getTime &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
