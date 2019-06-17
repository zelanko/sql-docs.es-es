---
title: Método insertRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.insertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 363d1008-1396-4fc0-8e27-c9ba2499e7f1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cf6b427cfaaf736fb7ea3862554bde172f2a0247
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66801228"
---
# <a name="insertrow-method-sqlserverresultset"></a>Método insertRow (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Agrega el contenido de la fila de inserción a este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) y a la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void insertRow()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método insertRow especificado por el método insertRow en la interfaz java.sql.ResultSet.  
  
 Cuando se llama a este método, el cursor debe estar en la fila de inserción. Una vez se llame a este método, el cursor permanece en la fila de inserción y el conjunto de resultados permanece en modo de inserción.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
