---
title: Método getNString (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 546d77e2-723a-42ac-ba3f-fabf2395d376
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0a76052ccf05927ebd598e2baa37fbf0229bf54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981397"
---
# <a name="getnstring-method-javalangstring-sqlserverresultset"></a>Método getNString (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor de la columna designada en la fila actual del objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un objeto java.lang.String.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getNString(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 Un valor String que contiene la etiqueta de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto de cadena.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método getNString especifica este método getNString en la interfaz java.sql.SQLServerResultSet.  
  
 Este método se puede usar para recuperar el valor de una columna **nvarchar**, **nchar**, **nvarchar (Max)** , **ntext**o **XML** en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) . Si intenta utilizar este método para recuperar valores de otros tipos de datos, se producirá una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Método getNString &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
