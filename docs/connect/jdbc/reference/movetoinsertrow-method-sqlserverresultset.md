---
title: Método moveToInsertRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.moveToInsertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3c54bfe-d5b7-4f6e-ae6c-3e8954e5b1c9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bc8420b9f79ce61874dbb03e73924e7be6eca96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976782"
---
# <a name="movetoinsertrow-method-sqlserverresultset"></a>Método moveToInsertRow (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Mueve el cursor a la fila de inserción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void moveToInsertRow()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método moveToInsertRow se especifica mediante el método moveToInsertRow de la interfaz java. SQL. ResultSet.  
  
 Se recuerda la posición del cursor actual mientras el cursor se coloca en la fila de inserción. La fila de inserción es una fila especial que está asociada a un conjunto de resultados con capacidad de actualización. Se trata básicamente de un búfer donde se puede generar una nueva fila si se llama a los métodos updater antes de agregar la fila al conjunto de resultados.  
  
 Solamente se puede llamar los métodos updater, getter e [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) cuando el cursor está en la fila de inserción. Se debe proporcionar un valor para todas las columnas en un conjunto de resultados cada vez que se llame a este método y antes de llamar a insertRow. Se debe llamar a un método updater antes de poder llamar a un método getter en un valor de columna.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
