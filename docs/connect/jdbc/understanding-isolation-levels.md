---
title: Descripción de los niveles de aislamiento | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2c41e23a-da6c-4650-b5fc-b5fe53ba65c3
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0115d8c16c63882990a462c0fde8d146e91dbf88
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="understanding-isolation-levels"></a>Descripción de los niveles de aislamiento
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Las transacciones especifican un nivel de aislamiento que define el grado en que se debe aislar una transacción de las modificaciones de recursos o datos realizadas por otras transacciones. Los niveles de aislamiento se describen en función de los efectos secundarios de la simultaneidad que se permiten, como las lecturas de datos sucios o las lecturas fantasmas.  
  
 Los niveles de aislamiento de transacciones controlan lo siguiente:  
  
-   Controla si se realizan bloqueos cuando se leen los datos y qué tipos de bloqueos se solicitan.  
  
-   Duración de los bloqueos de lectura.  
  
-   Si una operación de lectura que hace referencia a filas modificadas por otra transacción:  
  
    -   Se bloquea hasta que se libera el bloqueo exclusivo de la fila.  
  
    -   Recupera la versión confirmada de la fila que existía en el momento en el que se inició la instrucción o la transacción.  
  
    -   Lee la modificación de los datos no confirmada.  
  
 La selección de un nivel de aislamiento de transacción no afecta a los bloqueos adquiridos para proteger las modificaciones de datos. Una transacción siempre obtiene un bloqueo exclusivo en todos los datos se modifica y retiene ese bloqueo hasta que finalice la transacción, independientemente del nivel de aislamiento configurado para la transacción. En el caso de las operaciones de lectura, los niveles de aislamiento de transacción definen básicamente el nivel de protección contra los efectos de las modificaciones que realizan otras transacciones.  
  
 Un nivel de aislamiento menor significa que los usuarios tienen un mayor acceso a los datos simultáneamente, con lo que aumentan los efectos de la simultaneidad que pueden experimentar, como las lecturas de datos sucios o la pérdida de actualizaciones. Por el contrario, un nivel de aislamiento mayor reduce los tipos de efectos de simultaneidad, pero requiere más recursos del sistema y aumenta las posibilidades de que una transacción bloquee a otra. El nivel de aislamiento apropiado depende del equilibrio entre los requisitos de integridad de los datos de la aplicación y la sobrecarga de cada nivel de aislamiento. El nivel de aislamiento superior, que es serializable, garantiza que una transacción recuperará exactamente los mismos datos cada vez que repita una operación de lectura, aunque para ello aplicará un nivel de bloqueo que puede afectar a los demás usuarios en los sistemas multiusuario. El nivel de aislamiento menor, de lectura sin confirmar, puede recuperar datos que otras transacciones han modificado pero no confirmado. En este nivel se pueden producir todos los efectos secundarios de simultaneidad, pero no hay bloqueos ni versiones de lectura, por lo que la sobrecarga se reduce.  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente se muestran los efectos secundarios de la simultaneidad que permiten los distintos niveles de aislamiento.  
  
|Nivel de aislamiento|Lectura de datos sucios|lectura no repetible|Fantasma|  
|---------------------|----------------|-------------------------|-------------|  
|Lectura no confirmada|Sí|Sí|Sí|  
|Lectura confirmada|no|Sí|Sí|  
|Lectura repetible|no|No|Sí|  
|Snapshot|no|No|no|  
|Serializable|no|No|no|  
  
 Las transacciones se deben ejecutar en un nivel de aislamiento de lectura repetible, al menos, para evitar las pérdidas de actualizaciones que pueden producirse cuando dos transacciones recuperan la misma fila, y a continuación la actualizan según los valores recuperados originalmente. Si las dos transacciones actualizan las filas con una única instrucción UPDATE y no basan la actualización en los valores recuperados previamente, la pérdida de las actualizaciones no puede producirse en el nivel de aislamiento predeterminado de lectura confirmada.  
  
 Para establecer el nivel de aislamiento de una transacción, puede usar el [setTransactionIsolation](../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md) método de la [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase. Este método acepta un **int** valor como argumento, que se basa en una de las constantes de conexión como en el siguiente ejemplo:  
  
```  
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED);  
```  
  
 Para usar el nuevo nivel de aislamiento de instantánea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede utilizar una de las constantes de SQLServerConnection como en el siguiente ejemplo:  
  
```  
con.setTransactionIsolation(SQLServerConnection.TRANSACTION_SNAPSHOT);  
```  
  
 o puede utilizar:  
  
```  
con.setTransactionIsolation(Connection.TRANSACTION_READ_COMMITTED + 4094);  
```  
  
 Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] niveles de aislamiento, vea "niveles de aislamiento en el [!INCLUDE[ssDE](../../includes/ssde_md.md)]" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Realizar transacciones con el controlador JDBC](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)  
  
  
