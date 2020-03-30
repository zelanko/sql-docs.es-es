---
title: Método updateBigDecimal (int, java.math.BigDecimal) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateBigDecimal (int, java.math.BigDecimal)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1e15de27-a490-45cd-a3a6-a49721f15a97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad5239c609e58750e7fd494d482ee11c62ab9cc8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67985449"
---
# <a name="updatebigdecimal-method-int-javamathbigdecimal"></a>Método updateBigDecimal (int, java.math.BigDecimal)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un objeto BigDecimal según el índice de la columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateBigDecimal(int index,  
                             java.math.BigDecimal x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *índice*  
  
 Valor **int** que indica el índice de la columna.  
  
 *x*  
  
 Un objeto BigDecimal.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método updateBigDecimal especifica este método updateBigDecimal en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte también  
 [Método updateBigDecimal &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
