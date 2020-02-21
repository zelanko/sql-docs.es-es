---
title: Método getNCharacterStream (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f1cfa4e4-3e1f-4504-b0de-cc626d653661
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 004f5d89eaaa4293ae7da0058733b261c01c7531
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67981694"
---
# <a name="getncharacterstream-method-int-sqlserverresultset"></a>Método getNCharacterStream (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor de una columna designada en la fila actual del objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un objeto Reader.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.Reader getNCharacterStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Valor **int** que indica el índice de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Reader.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getNCharacterStream especifica este método getNCharacterStream en la interfaz java.sql.ResultSet.  
  
 Este método se puede usar para recuperar el valor de una columna **nvarchar**, **nchar**, **nvarchar(max)** , **ntext** o **xml** en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md). Si intenta utilizar este método para recuperar valores de otros tipos de datos, se producirá una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Método getNCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
