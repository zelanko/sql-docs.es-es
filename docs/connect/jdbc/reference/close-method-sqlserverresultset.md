---
title: Método Close (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.close
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8f3adf5b-874e-4cf2-b4ef-672dda42d77a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec9b51d08e10df0f829308d163b573c0670c78e7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637263"
---
# <a name="close-method-sqlserverresultset"></a>Método close (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Libera inmediatamente la base de datos de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) y los recursos de JDBC en lugar de esperar a que esto se realice cuando se cierre de forma automática.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void close()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método close especifica este método close en la interfaz java.sql.ResultSet.  
  
 Un objeto SQLServerResultSet se cierra automáticamente por el objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) que lo generó cuando ese objeto SQLServerStatement se cierra, se vuelve a utilizar o se utiliza para recuperar el siguiente resultado en un flujo de varios resultados. También se cierra un objeto SQLServerResultSet automáticamente cuando se recopila como elemento no utilizado.  
  
 Cuando se ejecuta una instrucción que genera un conjunto de resultados grande de solo avance y solo lectura, es posible que únicamente esté interesado en algún conjunto inicial de filas en el conjunto de resultados que se ha devuelto. En este caso, la aplicación podría llamar al método [cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md) del objeto de instrucción asociado antes de cerrar el conjunto de resultados con el fin de minimizar el tiempo de procesamiento necesario para descartar las filas innecesarias restantes. Recomendamos comparar los inconvenientes entre el tiempo de procesamiento que se ahorraría y el tiempo y el viaje de ida y vuelta al servidor que se necesita para cancelar la ejecución a la hora de decidir si utilizar o no esta técnica.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
