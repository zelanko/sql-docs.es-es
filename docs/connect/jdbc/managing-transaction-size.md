---
title: Administrar el tamaño de la transacción | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 82900342-bc80-445f-98a4-468a303aae1e
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 52401e2f9f360d8ec1867daa74fbc3b850995b19
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="managing-transaction-size"></a>Administrar el tamaño de las transacciones
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando trabaja con transacciones, es importante intentar que su tamaño sea el menor posible. El modo predeterminado de confirmación automática, que puede habilitar o deshabilitar mediante la [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md) método, confirmará cada acción. Éste es el modo más fácil en que trabajan la mayoría de los programadores.  
  
 Cuando use transacciones manuales, asegúrese de que el código confirma la transacción tan rápidamente como sea posible. Si se mantiene abierta una transacción, se impide que otros usuarios tengan acceso a los datos. Por ejemplo, una práctica aconsejable de programación sería poner una llamada para revertir en el bloque catch y una llamada para confirmar en el bloque finally. Sin embargo, esto depende del diseño de la aplicación.  
  
 Cuando las transacciones mantienen un tamaño reducido, se mejora la simultaneidad. Por ejemplo, si inicia una transacción manual y modifica 10.000 filas en una tabla de 20.000, tendrá la mitad de la tabla bloqueada completamente para todos los demás usuarios, aun cuando sólo estén leyendo los datos. Si reduce las modificaciones a 2.000 filas, se deja disponible el 90 por ciento de la tabla.  
  
 Además, asegúrese de utilizar el valor de tiempo de espera para la exclusión si la aplicación prevé que va a haber problemas de bloqueo y será necesario establecer tiempos de espera para solucionarlos. Puede hacerlo mediante el uso de la [setLockTimeout](../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md) método. El valor predeterminado del tiempo de espera para la exclusión es -1, lo que significa que el bloqueo se mantendrá indefinidamente mientras se espera la exclusión. Puede establecer el tiempo de espera para la exclusión en 30 segundos, lo que hará que la conexión bloqueada agote el tiempo de espera después de 30 segundos si otra conexión la bloquea.  
  
## <a name="see-also"></a>Vea también  
 [Mejorar el rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
