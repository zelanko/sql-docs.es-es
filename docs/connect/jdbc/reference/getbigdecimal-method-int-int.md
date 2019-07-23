---
title: Método getBigDecimal (int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBigDecimal (int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d9351b35-7046-4852-a612-72d4c46b2bbb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77fa7092b7835e400b7ced8c7dbc0368188b0eb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954005"
---
# <a name="getbigdecimal-method-int-int"></a>Método getBigDecimal (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como java.math.BigDecimal según el índice de parámetro y la escala.  
  
> [!NOTE]  
>  Este método se ha dejado de incluir en las especificaciones de JDBC. En su lugar, debería utilizar el método [getBigDecimal (int)](../../../connect/jdbc/reference/getbigdecimal-method-int.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.math.BigDecimal getBigDecimal(int index,  
                                          int scale)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Un valor **int** que indica el índice del parámetro.  
  
 *escala*  
  
 Valor **int** que indica el número de dígitos a la derecha del signo decimal.  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto BigDecimal.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getBigDecimal se especifica mediante el método getBigDecimal de la interfaz java. SQL. CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método getBigDecimal &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbigdecimal-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
