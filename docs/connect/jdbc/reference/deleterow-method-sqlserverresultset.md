---
title: Método deleteRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.deleteRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 987be5ee9fd49385acf02e52108e1e657fbc08a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66786519"
---
# <a name="deleterow-method-sqlserverresultset"></a>Método deleteRow (SQLServerResultSet)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Elimina la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) y de la base de datos subyacente.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
public void deleteRow()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método deleteRow especificado por el método deleteRow en la interfaz java.sql.ResultSet.  
  
 No se puede llamar a este método cuando el cursor está en la fila de inserción.  
  
 Al utilizar los cursores del conjunto de claves, este método deja un intervalo en el conjunto de resultados. Puede probar este intervalo mediante el método [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md). Los números de fila de las filas en el conjunto de resultados no se ven modificados.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
