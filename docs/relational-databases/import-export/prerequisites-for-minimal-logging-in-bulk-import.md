---
title: Requisitos previos para el registro mínimo durante la importación masiva | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- minimal logging [SQL Server]
- logged bulk copy [SQL Server]
- logs [SQL Server], minimal logging
- minimally logged operations [SQL Server]
- bulk importing [SQL Server], minimal logging
ms.assetid: bd1dac6b-6ef8-4735-ad4e-67bb42dc4f66
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 48d62232c5d481ccbb6204f5ba14465dea75ca30
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2019
ms.locfileid: "64946573"
---
# <a name="prerequisites-for-minimal-logging-in-bulk-import"></a>Requisitos previos para el registro mínimo durante la importación masiva
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En el caso de las bases de datos que utilizan el modelo de recuperación completa, todas las operaciones de inserción de filas que se efectúan durante la importación masiva se registran por completo en el registro de transacciones. Las importaciones de datos de gran volumen pueden hacer que el registro de transacciones se llene rápidamente si se utiliza el modelo de recuperación completa. En cambio, bajo el modelo de recuperación simple o el modelo de recuperación optimizado para cargas masivas de registros, el registro mínimo de operaciones de importaciones masivas reduce la posibilidad de que una de estas operaciones acabe con el espacio del registro. Además, el registro mínimo es más eficaz que el completo.  
  
> [!NOTE]  
>  El modelo de recuperación optimizado para cargas masivas de registros está diseñado para reemplazar temporalmente al modelo de recuperación completa durante operaciones masivas de gran tamaño.  
  
## <a name="table-requirements-for-minimally-logging-bulk-import-operations"></a>Requisitos de las tablas para las operaciones de importación masiva de registro mínimo  
 El registro mínimo exige que la tabla de destino cumpla las condiciones siguientes:  
  
-   La tabla no se está replicando.  
  
-   Se ha especificado el bloqueo de tabla (mediante TABLOCK). Para la tabla con índice de almacén de columnas en clúster, no necesita TABLOCK para el registro mínimo.  Además, solo se crean registros mínimos de los datos cargados en grupos de filas comprimidos, para lo que se requiere un tamaño de lote de 102 400 o más.  
  
    > [!NOTE]  
    >  Aunque no se registren las inserciones de datos en el registro de transacciones cuando se realiza una importación masiva de registro mínimo, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] seguirá registrando las asignaciones de extensiones cada vez que se asigne una nueva a la tabla.  
  
-   La tabla no está optimizada para memoria.  
  
 La posibilidad de utilizar el registro mínimo con una tabla también depende de si la tabla está indizada y, en este caso, de si está vacía:  
  
-   Si la tabla no tiene índices, el registro de las páginas de datos será mínimo.  
  
-   Si la tabla no tiene índice clúster sino uno o más índices no clúster, el registro de las páginas de datos siempre será mínimo. Sin embargo, el modo en que se registran las páginas de índice depende de si la tabla está vacía:  
  
    -   Si la tabla está vacía, el registro de las páginas de índice será mínimo.  
  
    -   Si la tabla no está vacía, el registro de las páginas de índice será completo.  
  
        > [!NOTE]  
        >  Si empieza con una tabla vacía y realiza una importación masiva de datos mediante varios lotes, el registro de las páginas de índice y de datos será mínimo para el primer lote pero, a partir del segundo lote, solo las páginas de datos se registrarán de forma mínima.  
  
-   Si la tabla tiene un índice clúster y está vacía, tanto las páginas de datos como de índice se registrarán de forma mínima. En cambio, si la tabla tiene un índice en clúster basado en btree pero no está vacía, tanto las páginas de datos como las de índice se registrarán de forma completa, independientemente del modelo de recuperación utilizado. Para las tablas con índices de almacén de columnas en clúster, los registros mínimos de los datos cargados en grupos de filas comprimidos siempre se realizan con independencia de que la tabla esté vacía o no cuando el tamaño es igual o superior a 102 400.  
  
    > [!NOTE]  
    >  Si empieza con una tabla de almacén de filas vacía y realiza una importación masiva de datos mediante varios lotes, el registro de las páginas de índice y de datos será mínimo para el primer lote pero, a partir del segundo lote, solo las páginas de datos se registrarán de forma mínima.  
  
> [!NOTE]  
>  Cuando la replicación transaccional está habilitada, las operaciones BULK INSERT se registran por completo en el modelo de recuperación optimizado para cargas masivas de registros.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Ver o cambiar el modelo de recuperación de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
  
## <a name="see-also"></a>Consulte también  
 [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
  
  
