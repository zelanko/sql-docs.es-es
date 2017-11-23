---
title: Las instrucciones | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: e6e36b056aaca063970c81d2932ec47ee7cef29e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="transact-sql-statements"></a>Instrucciones Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

Este tema de referencia resume las categorías de instrucciones para su uso con Transact-SQL (T-SQL). Puede encontrar todas las instrucciones que aparecen en el panel de navegación izquierdo.

## <a name="backup-and-restore"></a>Copias de seguridad y restauración
Las instrucciones backup y restore proporcionan formas de crear copias de seguridad y restauración de copias de seguridad.  Para obtener más información, consulte el [información general de copia de seguridad y restauración](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).

## <a name="data-definition-language"></a>Lenguaje de definición de datos
Las instrucciones de lenguaje de definición (DDL) de datos define las estructuras de datos. Use estas instrucciones para crear, modificar o quitar estructuras de datos en una base de datos.
- ALTER
- Intercalaciones
- CREATE
- DROP
- DESHABILITAR EL DESENCADENADOR
- ENABLE TRIGGER
- CAMBIAR EL NOMBRE
- ACTUALIZAR ESTADÍSTICAS

## <a name="data-manipulation-language"></a>Lenguaje de manipulación de datos
Lenguaje de manipulación de datos (DML) afectan a la información almacenada en la base de datos. Use estas instrucciones para insertar, actualizar y cambiar las filas de la base de datos.

- BULK INSERT
- DELETE
- INSERT
- MERGE
- TRUNCATE TABLE

## <a name="permissions-statements"></a>Instrucciones de permisos
Instrucciones de permisos determinan qué usuarios y los inicios de sesión pueden tener acceso a datos y realizar operaciones. Para obtener más información sobre la autenticación y acceso, consulte el [centro de seguridad](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="service-broker-statements"></a>Instrucciones de Service Broker
Service Broker es una característica que proporciona compatibilidad nativa para las aplicaciones de mensajes y puesta en cola. Para obtener más información, consulte [Service Broker](../../relational-databases/service-broker/event-notifications.md).

## <a name="session-settings"></a>Configuración de sesión
Instrucciones SET determinan cómo los identificadores de sesión actual los parámetros de tiempo de ejecución. Para obtener información general, vea [instrucciones SET](set-statements-transact-sql.md).
