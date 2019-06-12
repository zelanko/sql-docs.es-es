---
title: Información general sobre transacciones | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ad6ccc7f65d6d4c65fb1bb63b58e0b13269ea351
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66788402"
---
# <a name="understanding-transactions"></a>Descripción de transacciones

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Las transacciones son grupos de operaciones que se combinan en unidades lógicas de trabajo. Se usan para controlar y mantener la coherencia y la integridad de cada acción de una transacción, a pesar de los errores que puedan producirse en el sistema,

Con [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], las transacciones pueden ser locales o distribuidas. Las transacciones también pueden usar niveles de aislamiento. Para obtener más información acerca de los niveles de aislamiento compatibles con el controlador JDBC, vea [Descripción de los niveles de aislamiento](../../connect/jdbc/understanding-isolation-levels.md).

LAs aplicaciones deben controlar las transacciones usando las instrucciones Transact-SQ o los métodos proporcionados por el controlador JDBC, pero no ambos. Usar en la misma transacción las instrucciones Transact-SQL y los métodos API de JDBC podría producir problemas, como que una transacción no pueda ser confirmada cuando se espera, que la transacción sea confirmada o se revierta y se inicie una nueva inesperadamente, o las excepciones "No se pudo reanudar la transacción".

## <a name="using-local-transactions"></a>Usar transacciones locales

Se considera que una transacción es local cuando es de una sola fase y la base de datos la trata directamente. El controlador JDBC es compatible con las transacciones locales mediante el uso de varios métodos de la clase [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md), incluidos [setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md), [commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) y [rollback](../../connect/jdbc/reference/rollback-method.md). Las transacciones locales suelen ser administradas explícitamente por la aplicación o automáticamente por el servidor de aplicaciones de Java Platform, Enterprise Edition (Java EE).

El siguiente ejemplo realiza una transacción local que se compone de dos instrucciones separadas en el bloque `try`. Las instrucciones se ejecutan en la tabla Production.ScrapReason de la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] y se confirman si no se lanza ninguna excepción. El código del bloque `catch` revierte la transacción si se lanza una excepción.

[!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]

## <a name="using-distributed-transactions"></a>Usar transacciones distribuidas

Una transacción distribuida es una transacción que actualiza datos en dos o más bases de datos conectadas a una red manteniendo las propiedades atómicas, coherentes, aisladas y durables (ACID) del procesamiento de la transacción. La compatibilidad con las transacciones distribuidas se incluyó en la API de JDBC de la especificación API Opcional de JDBC 2.0. La administración de transacciones distribuidas normalmente se realiza de forma automática por parte del administrador de transacciones Servicio de Transacciones de Java (JTS) dentro de un entorno de servidor de aplicaciones Java EE. No obstante, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite las transacciones distribuidas realizadas en cualquier administrador de transacciones compatible con la API de transacciones de Java (JTA).

El controlador JDBC se integra a la perfección con el Coordinador de transacciones distribuidas (MS DTC) de [!INCLUDE[msCoName](../../includes/msconame_md.md)] para proporcionar una compatibilidad real con las transacciones distribuidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. MS DTC es una herramienta de transacciones distribuidas que proporciona [!INCLUDE[msCoName](../../includes/msconame_md.md)] para sistemas [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows. MS DTC usa tecnología probada de procesamiento de transacciones de [!INCLUDE[msCoName](../../includes/msconame_md.md)] para proporcionar compatibilidad con características XA tales como el protocolo de confirmación distribuido de dos fases completo y la recuperación de transacciones distribuidas.

Para obtener más información sobre cómo utilizar las transacciones distribuidas, consulte [Descripción de las transacciones XA](../../connect/jdbc/understanding-xa-transactions.md).

## <a name="see-also"></a>Consulte también

[Realizar transacciones con el controlador JDBC](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
