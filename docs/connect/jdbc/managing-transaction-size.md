---
title: Administración del tamaño de las transacciones | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 82900342-bc80-445f-98a4-468a303aae1e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14729ba2782bfd9f88e718fbde50de30ae13e645
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923096"
---
# <a name="managing-transaction-size"></a>Administración del tamaño de las transacciones
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cuando trabaja con transacciones, es importante intentar que su tamaño sea el menor posible. El modo predeterminado de confirmación automática, que puede habilitar o deshabilitar con el método [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md), confirmará cada acción en su lugar. Éste es el modo más fácil en que trabajan la mayoría de los programadores.  
  
 Cuando use transacciones manuales, asegúrese de que el código confirma la transacción tan rápidamente como sea posible. Si se mantiene abierta una transacción, se impide que otros usuarios tengan acceso a los datos. Por ejemplo, una práctica aconsejable de programación sería poner una llamada para revertir en el bloque catch y una llamada para confirmar en el bloque finally. Sin embargo, esto depende del diseño de la aplicación.  
  
 Cuando las transacciones mantienen un tamaño reducido, se mejora la simultaneidad. Por ejemplo, si inicia una transacción manual y modifica 10.000 filas en una tabla de 20.000, tendrá la mitad de la tabla bloqueada completamente para todos los demás usuarios, aun cuando sólo estén leyendo los datos. Si reduce las modificaciones a 2.000 filas, se deja disponible el 90 por ciento de la tabla.  
  
 Además, asegúrese de utilizar el valor de tiempo de espera para la exclusión si la aplicación prevé que va a haber problemas de bloqueo y será necesario establecer tiempos de espera para solucionarlos. Para ello, puede usar el método [setLockTimeout](../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md). El valor predeterminado del tiempo de espera para la exclusión es -1, lo que significa que el bloqueo se mantendrá indefinidamente mientras se espera la exclusión. Puede establecer el tiempo de espera para la exclusión en 30 segundos, lo que hará que la conexión bloqueada agote el tiempo de espera después de 30 segundos si otra conexión la bloquea.  
  
## <a name="see-also"></a>Consulte también  
 [Mejora del rendimiento y la confiabilidad con el controlador JDBC](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
