---
title: Instrucciones | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d8d6f62a-e815-425c-a80e-a63fd34ec275
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 43d4405411005ab43e3f2b2fe9b2136a5793e8a5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68099981"
---
# <a name="transact-sql-statements"></a>Instrucciones Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

En este tema se resumen las categorías de instrucciones para utilizar con Transact-SQL (T-SQL). Puede encontrar todas las instrucciones que aparecen en el panel de navegación izquierdo.

## <a name="backup-and-restore"></a>Copia de seguridad y restauración
Las instrucciones de copia de seguridad y restauración proporcionan formas de crear copias de seguridad y restauración a partir de copias de seguridad.  Para obtener más información, consulte [Realizar copias de seguridad y restaurar bases de datos](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).

## <a name="data-definition-language"></a>Lenguaje de definición de datos
Las instrucciones del lenguaje de definición de datos (DDL) definen estructuras de datos. Use estas instrucciones para crear, modificar o quitar estructuras de datos en una base de datos.
- ALTER
- Intercalaciones
- CREATE
- DROP
- DISABLE TRIGGER
- ENABLE TRIGGER
- RENAME
- UPDATE STATISTICS

## <a name="data-manipulation-language"></a>Lenguaje de manipulación de datos
El lenguaje de manipulación de datos (DML) afecta a la información almacenada en la base de datos. Use estas instrucciones para insertar, actualizar y cambiar las filas de la base de datos.

- BULK INSERT
- Delete
- INSERT
- UPDATE
- MERGE
- TRUNCATE TABLE

## <a name="permissions-statements"></a>Instrucciones de permisos
Las instrucciones de permisos determinan qué usuarios e inicios de sesión pueden tener acceso a datos y realizar operaciones. Para obtener más información sobre la autenticación y el acceso, consulte el [Centro de seguridad](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="service-broker-statements"></a>Instrucciones de Service Broker
Service Broker es una característica que proporciona compatibilidad nativa para las aplicaciones de mensajería y de cola. Para obtener más información, vea [Service Broker](../../relational-databases/service-broker/event-notifications.md).

## <a name="session-settings"></a>Configuración de sesión
Las instrucciones SET determinan de qué forma la sesión actual gestiona las opciones de configuración del tiempo de ejecución. Para obtener información general, vea [Instrucciones SET](set-statements-transact-sql.md).
