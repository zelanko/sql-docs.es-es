---
title: Método setString (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 25dabdc9-c60f-485a-87eb-306067964765
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ca49c8e50527ab7cafce9c93c314a0e363b45402
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67972584"
---
# <a name="setstring-method-sqlserverpreparedstatement"></a>Método setString (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el valor **String** indicado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setString(int index,  
                            java.lang.String str)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *índice*  
  
 Valor **int** que indica el número de parámetro.  
  
 *str*  
  
 Un valor **String**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setString especifica este método setString en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
