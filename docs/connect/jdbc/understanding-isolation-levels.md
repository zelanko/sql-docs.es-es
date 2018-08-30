---
title: Descripción de los niveles de aislamiento | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2c41e23a-da6c-4650-b5fc-b5fe53ba65c3
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4a91678f90164a85907a21f50d74b50561ceaff
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42784822"
---
# <a name="understanding-isolation-levels"></a>Descripción de los niveles de aislamiento

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Las transacciones especifican un nivel de aislamiento que define el grado en que se debe aislar una transacción de las modificaciones de recursos o datos realizadas por otras transacciones. Los niveles de aislamiento se describen en función de los efectos secundarios de la simultaneidad que se permiten, como las lecturas de datos sucios o las lecturas fantasmas.  
  
Los niveles de aislamiento de transacciones controlan lo siguiente:  
  
- Controla si se realizan bloqueos cuando se leen los datos y qué tipos de bloqueos se solicitan.  
  
- Duración de los bloqueos de lectura.  
  
- Si una operación de lectura que hace referencia a filas modificadas por otra transacción:  
  
  - Se bloquea hasta que se libera el bloqueo exclusivo de la fila.  
  
  - Recupera la versión confirmada de la fila que existía en el momento en el que se inició la instrucción o la transacción.  
  
  - Lee la modificación de los datos no confirmada.  

La selección de un nivel de aislamiento de transacción no afecta a los bloqueos adquiridos para proteger las modificaciones de datos. Siempre se obtiene un bloqueo exclusivo en los datos modificados de una transacción, bloqueo que se mantiene hasta que se completa la transacción, independientemente del nivel de aislamiento seleccionado para la misma. En el caso de las operaciones de lectura, los niveles de aislamiento de transacción definen básicamente el nivel de protección contra los efectos de las modificaciones que realizan otras transacciones.  
  
Un nivel de aislamiento menor significa que los usuarios tienen un mayor acceso a los datos simultáneamente, con lo que aumentan los efectos de la simultaneidad que pueden experimentar, como las lecturas de datos sucios o la pérdida de actualizaciones. Por el contrario, un nivel de aislamiento mayor reduce los tipos de efectos de simultaneidad, pero requiere más recursos del sistema y aumenta las posibilidades de que una transacción bloquee a otra. El nivel de aislamiento apropiado depende del equilibrio entre los requisitos de integridad de los datos de la aplicación y la sobrecarga de cada nivel de aislamiento. El nivel de aislamiento superior, que es serializable, garantiza que una transacción recuperará exactamente los mismos datos cada vez que repita una operación de lectura, aunque para ello aplicará un nivel de bloqueo que puede afectar a los demás usuarios en los sistemas multiusuario. El nivel de aislamiento menor, de lectura sin confirmar, puede recuperar datos que otras transacciones han modificado pero no confirmado. En este nivel se pueden producir todos los efectos secundarios de simultaneidad, pero no hay bloqueos ni versiones de lectura, por lo que la sobrecarga se reduce.  

## <a name="remarks"></a>Notas

 En la tabla siguiente se muestran los efectos secundarios de la simultaneidad que permiten los distintos niveles de aislamiento.  
  
| Nivel de aislamiento  | Lectura de datos sucios | lectura no repetible | Fantasma |
| ---------------- | ---------- | ------------------- | ------- |
| Lectura no confirmada | Sí        | Sí                 | Sí     |
| Lectura confirmada   | no         | Sí                 | Sí     |
| Lectura repetible  | no         | no                  | Sí     |
| Snapshot         | no         | no                  | no      |
| Serializable     | no         | no                  | no      |
  
Las transacciones se deben ejecutar en un nivel de aislamiento de lectura repetible, al menos, para evitar las pérdidas de actualizaciones que pueden producirse cuando dos transacciones recuperan la misma fila, y a continuación la actualizan según los valores recuperados originalmente. Si las dos transacciones actualizan las filas con una única instrucción UPDATE y no basan la actualización en los valores recuperados previamente, la pérdida de las actualizaciones no puede producirse en el nivel de aislamiento predeterminado de lectura confirmada.  

Para establecer el nivel de aislamiento para una transacción, puede utilizar el método de [setTransactionIsolation](../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). Este método acepta un valor **int** como argumento, que se basa en una de las constantes de conexión, según se muestra a continuación:  

```java
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);  
```

Para utilizar el nuevo nivel de aislamiento de instantánea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede utilizar una de las constantes `SQLServerConnection`:  

```java
con.setTransactionIsolation(SQLServerConnection.TRANSACTION_SNAPSHOT);  
```

o puede utilizar:  

```java
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED + 4094);  
```

Para obtener más información sobre los niveles de aislamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea "Niveles de aislamiento en [!INCLUDE[ssDE](../../includes/ssde_md.md)]" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="see-also"></a>Ver también

[Realizar transacciones con el controlador JDBC](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
