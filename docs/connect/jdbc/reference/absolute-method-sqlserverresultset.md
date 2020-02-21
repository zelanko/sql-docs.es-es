---
title: Método absolute (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.absolute
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 638e8148-8ca0-4e1f-9ec2-04a11bc9809b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 66bdbfa417077e70be7969b28ae851a0244e54ca
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67956066"
---
# <a name="absolute-method-sqlserverresultset"></a>Método absolute (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Mueve el cursor a la fila especificada en este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean absolute(int row)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *row*  
  
 Un valor **int** que indica el número de fila al que se va a desplazar. Puede ser positivo, negativo o 0.  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si el cursor se desplaza a la posición dada. **false** si es anterior a la primera fila o posterior a la última fila.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método absolute especifica este método absolute en la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
