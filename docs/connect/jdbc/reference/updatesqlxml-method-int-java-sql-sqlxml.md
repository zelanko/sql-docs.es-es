---
title: Método updateSQLXML (int, java.sql.SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b5170751-fbe1-433b-96f5-4f237ba55f60
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b7b602b0f23c1791ba76df3846fcc223716a0dd9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800186"
---
# <a name="updatesqlxml-method-int-javasqlsqlxml"></a>Método updateSQLXML (int, java.sql.SQLXML)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor java.sql.SQLXML  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateSQLXML(int columnIndex,  
                         java.sql.SQLXML xmlObject)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Valor **int** que indica el índice de la columna.  
  
 *xmlObject*  
  
 Un objeto SQLXML.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método updateSQLXML especificado por el método updateSQLXML de la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte también  
 [Método updateSQLXML &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
