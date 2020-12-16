---
title: Definición de la durabilidad de los objetos con optimización para memoria | Microsoft Docs
description: 'Obtenga información sobre las opciones de durabilidad para las tablas optimizadas para memoria en SQL Server: el SCHEMA_AND_DATA y el SCHEMA_ONLY predeterminados.'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 299695e0602b41623550a90e84aca9d6e6f633a2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481236"
---
# <a name="defining-durability-for-memory-optimized-objects"></a>Definir la durabilidad de los objetos con optimización para memoria
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Hay dos opciones de durabilidad para las tablas optimizadas para memoria:  
  
 SCHEMA_AND_DATA (predeterminado)  
 Esta opción proporciona durabilidad para el esquema y los datos. El nivel de durabilidad de los datos depende de si elige confirmar una transacción como totalmente durable o con durabilidad diferida. Las transacciones totalmente durables proporcionan la misma garantía de durabilidad tanto del esquema como de los datos, de forma similar a una tabla basada en disco. La durabilidad diferida mejorará el rendimiento pero podría provocar la pérdida de datos en caso de un bloqueo o una conmutación por error de servidor. (Para obtener más información sobre la durabilidad diferida, vea [Controlar la durabilidad de las transacciones](../../relational-databases/logs/control-transaction-durability.md)).  
  
 SCHEMA_ONLY  
 Esta opción garantiza la durabilidad del esquema de tabla. Cuando se reinicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o se produce una reconfiguración en una base de datos SQL de Azure, se conserva el esquema de tabla, pero se pierden los datos de la tabla. (Esto es distinto de una tabla en tempdb, donde tanto la tabla como sus datos se pierden al reiniciar). Un escenario típico para crear una tabla no durable es almacenar datos transitorios, como una tabla de ensayo para un proceso ETL. La durabilidad de SCHEMA_ONLY evita tanto el registro de transacciones como el punto de comprobación, lo que puede reducir significativamente las operaciones de E/S.  
  
 Cuando se usan las tablas predeterminadas SCHEMA_AND_DATA, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona la misma durabilidad que se garantiza para las tablas basadas en disco:  
  
 Durabilidad transaccional  
 Cuando se confirma una transacción totalmente durable que realizó cambios (DDL o DML) en una tabla optimizada para memoria, los cambios realizados en una tabla durable optimizada para memoria son permanentes.  
  
 Cuando se confirma una transacción diferida durable en una tabla optimizada para memoria, la transacción se convierte en perdurable solo después de que el registro de transacciones en memoria se guarde en el disco. (Para obtener más información sobre la durabilidad diferida, vea [Controlar la durabilidad de las transacciones](../../relational-databases/logs/control-transaction-durability.md)).  
  
 Durabilidad del reinicio  
 Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reinicia tras un cierre planeado o un bloqueo, se vuelve a crear una instancia de las tablas durables optimizadas para memoria para restaurarlas al estado anterior al cierre o al bloqueo.  
  
 Durabilidad de los errores de medios  
 Si un disco dañado o con errores contiene una o más copias conservadas de objetos optimizados para memoria durables, la característica de restauración y copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restaura las tablas optimizadas para memoria en los nuevos medios.  
  
## <a name="see-also"></a>Consulte también  
 [Crear y administrar el almacenamiento de objetos optimizados para memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
