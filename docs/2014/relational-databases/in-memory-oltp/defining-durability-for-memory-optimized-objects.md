---
title: Definición de la durabilidad de los objetos con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 80897eb2c4744a2dfd1253067f65eb0fd6429f50
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112919"
---
# <a name="defining-durability-for-memory-optimized-objects"></a>Definir la durabilidad de los objetos con optimización para memoria
  OLTP en memoria garantiza las propiedades completas de atomicidad, coherencia, aislamiento y durabilidad (ACID). La durabilidad en el contexto de las tablas optimizadas para memoria y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece las garantías siguientes:  
  
 Durabilidad transaccional  
 Cuando se confirma una transacción totalmente durable que realizó cambios (DDL o DML) en una tabla optimizada para memoria, los cambios realizados en una tabla durable optimizada para memoria son permanentes.  
  
 Cuando se confirma una transacción diferida durable en una tabla optimizada para memoria, la transacción se convierte en perdurable solo después de que el registro de transacciones en memoria se guarde en el disco.  
  
 Durabilidad del reinicio  
 Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reinicia tras un cierre planeado o un bloqueo, se vuelve a crear una instancia de las tablas durables optimizadas para memoria para restaurarlas al estado anterior al cierre o al bloqueo.  
  
 Durabilidad de los errores de medios  
 Si un disco dañado o con errores contiene una o más copias conservadas de objetos optimizados para memoria durables, la característica de restauración y copia de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restaura las tablas optimizadas para memoria en los nuevos medios.  
  
 Hay dos opciones de durabilidad para las tablas optimizadas para memoria:  
  
 SCHEMA_ONLY (tabla no durable)  
 Esta opción garantiza la durabilidad del esquema de tabla, incluidos los índices. Cuando se reinicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la tabla no durable se vuelve a crear pero se inicia sin datos. (Esto es distinto de una tabla en tempdb, donde tanto la tabla como sus datos se pierden al reiniciar). Un escenario típico para crear una tabla no durable es almacenar datos transitorios, como una tabla de ensayo para un proceso ETL. La durabilidad de SCHEMA_ONLY evita tanto el registro de transacciones como el punto de comprobación, lo que puede reducir significativamente las operaciones de E/S.  
  
 SCHEMA_AND_DATA (tabla durable)  
 Esta opción proporciona durabilidad para el esquema y los datos. El nivel de durabilidad de los datos depende de si elige confirmar una transacción como totalmente durable o con durabilidad diferida. Las transacciones totalmente durables proporcionan la misma garantía de durabilidad tanto del esquema como de los datos, de forma similar a una tabla basada en disco. La durabilidad diferida mejorará el rendimiento pero podría provocar la pérdida de datos en caso de un bloqueo o una conmutación por error de servidor. (Para obtener más información sobre la durabilidad diferida, vea [Controlar la durabilidad de las transacciones](../logs/control-transaction-durability.md)).  
  
 El esquema de la tabla optimizada para memoria se conserva, de forma similar a las tablas basadas en disco, en el grupo de archivos principal de una base de datos.  
  
 Los datos de las tablas optimizadas para memoria durables se guardan en pares de archivos delta y de datos.  
  
 Los índices definidos en las tablas optimizadas para memoria persisten solo en los metadatos, no en el almacenamiento. Las estructuras de índice se generan como parte de la carga de tablas optimizadas para memoria.  
  
 Las filas se eliminan explícitamente por medio de una instrucción DELETE o indirectamente por medio de una instrucción UPDATE. Se ejecuta una operación UPDATE como una eliminación seguida de una inserción. Cuando se elimina una fila, no se realiza ningún cambio en un archivo de datos pero se anexa una nueva fila, que identifica la fila eliminada, al archivo delta correspondiente.  
  
 Durante las operaciones de restauración o recuperación, el motor OLTP en memoria lee los archivos delta y de datos para cargarlos en la memoria física. El tiempo de carga está determinado por:  
  
-   Cantidad de datos que se van a cargar.  
  
-   Ancho de banda secuencial de E/S.  
  
-   Grado de paralelismo, determinado por el número de contenedores de archivos y de núcleos del procesador.  
  
-   La cantidad de entradas de registro en la parte activa del registro que tienen que rehacerse.  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar el almacenamiento de objetos con optimización para memoria](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  