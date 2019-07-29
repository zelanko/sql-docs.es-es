---
title: Método refreshRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.refreshRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 570a9185a83ecf1af0e47ee25cce5445dca1b958
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975978"
---
# <a name="refreshrow-method-sqlserverresultset"></a>Método refreshRow (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la fila actual con el valor más reciente en la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void refreshRow()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método refreshRow se especifica mediante el método refreshRow de la interfaz java. SQL. ResultSet.  
  
 No se puede llamar a este método cuando el cursor está en la fila de inserción.  
  
 Este método ofrece un sistema para que una aplicación indique explícitamente al controlador JDBC que vuelva a capturar filas desde la base de datos. Es posible que una aplicación necesite llamar a este método cuando el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] esté almacenando en memoria caché o efectuando una captura previa del último valor de una fila de la base de datos. El controlador JDBC podría actualizar varias filas a la vez si el tamaño de captura es mayor que uno.  
  
 Todos los valores se vuelven a capturar en función del nivel de aislamiento de transacción y sensibilidad de cursor. Si se llama a este método después de llamar a un método de actualización, pero antes de llamar al método [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md), las actualizaciones realizadas en la fila se perderán. Por lo general, si se llama a este método, el rendimiento será más lento.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
