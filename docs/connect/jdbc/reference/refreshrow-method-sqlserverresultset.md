---
title: "Método refreshRow (SQLServerResultSet) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerResultSet.refreshRow
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5f1a7c8a4a5381291d21f35adba178f05bc83f3f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
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
  
## <a name="remarks"></a>Comentarios  
 Este método refreshRow especificado por el método refreshRow en la interfaz java.sql.ResultSet.  
  
 No se puede llamar a este método cuando el cursor está en la fila de inserción.  
  
 Este método ofrece un sistema para que una aplicación indique explícitamente al controlador JDBC que vuelva a capturar filas desde la base de datos. Una aplicación necesite llamar a este método cuando el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] es el almacenamiento en caché o la captura previa para capturar el valor más reciente de una fila de la base de datos. El controlador JDBC podría actualizar varias filas a la vez si el tamaño de captura es mayor que uno.  
  
 Todos los valores se vuelven a capturar en función del nivel de aislamiento de transacción y sensibilidad de cursor. Si se llama a este método después de llamar a un método updater, pero antes de llamar a la [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) método, las actualizaciones realizadas en la fila se pierden. Por lo general, si se llama a este método, el rendimiento será más lento.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
