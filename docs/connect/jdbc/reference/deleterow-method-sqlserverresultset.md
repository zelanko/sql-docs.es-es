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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c6f5cc2d3b58f553f74288c2c86e7b6d9d32d72
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922163"
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
  
## <a name="remarks"></a>Observaciones  
 El método deleteRow especifica este método deleteRow en la interfaz java.sql.ResultSet.  
  
 No se puede llamar a este método cuando el cursor está en la fila de inserción.  
  
 Al utilizar los cursores del conjunto de claves, este método deja un intervalo en el conjunto de resultados. Puede probar este intervalo mediante el método [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md). Los números de fila de las filas en el conjunto de resultados no se ven modificados.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
