---
title: Uso de la retención | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e447b5b9e1e24e716122622cc5cff873a452b1f7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916246"
---
# <a name="using-holdability"></a>Usar la capacidad de alojamiento

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

De forma predeterminada, un conjunto de resultados creado dentro de una transacción se mantiene abierto cuando se ha confirmado la transacción a la base de datos o se ha revertido. No obstante, en ocasiones es útil que el conjunto de resultados esté cerrado, incluso después de haber confirmado la transacción. Para ello, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite el uso de la capacidad de alojamiento de conjuntos de resultados.

La capacidad de alojamiento de conjuntos de resultados se puede configurar con el método [setHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). A la hora de configurar la capacidad de alojamiento con el método setHoldability, se pueden usar las constantes de la capacidad de alojamiento del conjunto de resultados de `ResultSet.HOLD_CURSORS_OVER_COMMIT` o `ResultSet.CLOSE_CURSORS_AT_COMMIT`.

El controlador JDBC también es compatible con la configuración de la capacidad de alojamiento cuando se crea uno de los objetos Statement. Al crear los objetos Statement que tengan sobrecargas con los parámetros de la capacidad de alojamiento de los conjuntos de resultados, la capacidad de alojamiento del objeto de instrucción debe coincidir con la capacidad de alojamiento de la sobrecarga. Cuando no coinciden, se genera una excepción. Esto se debe a que SQL Server solamente admite la capacidad de alojamiento en el nivel de conexiones.

La capacidad de alojamiento de un conjunto de resultados es la capacidad de alojamiento del objeto SQLServerConnection asociado al conjunto de resultados en el momento en que se creó solamente para los cursores del servidor. Esto no se aplica a los cursores del lado cliente. Todos los conjuntos de resultados del lado cliente tendrán siempre el valor de capacidad de alojamiento de `ResultSet.HOLD_CURSORS_OVER_COMMIT`.

Para los cursores de servidor, cuando están conectados a SQL Server 2005 o versiones posteriores, la configuración de la capacidad de alojamiento solamente afecta a la de los nuevos conjuntos de resultados que todavía han de ser creados en esa conexión. Eso significa que la configuración de la capacidad de alojamiento no afecta a la capacidad de alojamiento de los conjuntos de resultados creados previamente que ya estaban abiertos en esa conexión.

En el siguiente ejemplo, se configura la capacidad de alojamiento del conjunto de resultados mientras se realiza una transición local que consiste en dos instrucciones independientes en el bloque `try`. Las instrucciones se ejecutan en la tabla Production.ScrapReason de la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Primero, el ejemplo cambia al modo de transacción manual configurando la confirmación automática en `false`. Una vez que el modo de confirmación automática está deshabilitado, no se confirman instrucciones SQL hasta que la aplicación llama explícitamente al método [commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md). El código del bloque catch revierte la transacción si se lanza una excepción.

[!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]

## <a name="see-also"></a>Consulte también

[Realizar transacciones con el controlador JDBC](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
