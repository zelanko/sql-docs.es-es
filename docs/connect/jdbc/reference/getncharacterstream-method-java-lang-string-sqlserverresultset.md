---
title: Método getNCharacterStream (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a117f3a3-9c25-41e1-9adb-a40e90620dd6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c2cd07b0420d8ca961c61c205c94cd19fe6666e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981639"
---
# <a name="getncharacterstream-method-javalangstring-sqlserverresultset"></a>Método getNCharacterStream (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor de la columna designada en la fila actual del objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un objeto Reader.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 Un valor String que contiene la etiqueta de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto de lector.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getNCharacterStream se especifica mediante el método getNCharacterStream de la interfaz java. SQL. ResultSet.  
  
 Este método se puede usar para recuperar el valor de una columna **nvarchar**, **nchar**, **nvarchar (Max)** , **ntext**o **XML** en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) . Si intenta utilizar este método para recuperar valores de otros tipos de datos, se producirá una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Método getNCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
