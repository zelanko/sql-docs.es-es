---
title: "Requisitos previos para el registro m&#237;nimo durante la importaci&#243;n masiva | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "registro mínimo [SQL Server]"
  - "copia por medio de registros de operaciones masivas [SQL Server]"
  - "registros [SQL Server], registro mínimo"
  - "registro mínimo, operaciones"
  - "importación en bloque [SQL Server], registro mínimo"
ms.assetid: bd1dac6b-6ef8-4735-ad4e-67bb42dc4f66
caps.latest.revision: 48
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 47
---
# Requisitos previos para el registro m&#237;nimo durante la importaci&#243;n masiva
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  En el caso de las bases de datos que utilizan el modelo de recuperación completa, todas las operaciones de inserción de filas que se efectúan durante la importación masiva se registran por completo en el registro de transacciones. Las importaciones de datos de gran volumen pueden hacer que el registro de transacciones se llene rápidamente si se utiliza el modelo de recuperación completa. En cambio, bajo el modelo de recuperación simple o el modelo de recuperación optimizado para cargas masivas de registros, el registro mínimo de operaciones de importaciones masivas reduce la posibilidad de que una de estas operaciones acabe con el espacio del registro. Además, el registro mínimo es más eficaz que el completo.  
  
> [!NOTE]  
>  El modelo de recuperación optimizado para cargas masivas de registros está diseñado para reemplazar temporalmente al modelo de recuperación completa durante operaciones masivas de gran tamaño.  
  
## Requisitos de las tablas para las operaciones de importación masiva de registro mínimo  
 El registro mínimo exige que la tabla de destino cumpla las condiciones siguientes:  
  
-   La tabla no se está replicando.  
  
-   Se ha especificado el bloqueo de tabla (mediante TABLOCK). Para la tabla con índice de almacén de columnas en clúster, no necesita TABLOCK para el registro mínimo.  Además, solo se crean registros mínimos de los datos cargados en grupos de filas comprimidos, para lo que se requiere un tamaño de lote de 102 400 o más.  
  
    > [!NOTE]  
    >  Aunque no se registren las inserciones de datos en el registro de transacciones cuando se realiza una importación masiva de registro mínimo, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] seguirá registrando las asignaciones de extensiones cada vez que se asigne una nueva a la tabla.  
  
-   La tabla no es con optimización para memoria.  
  
 La posibilidad de utilizar el registro mínimo con una tabla también depende de si la tabla está indizada y, en este caso, de si está vacía:  
  
-   Si la tabla no tiene índices, el registro de las páginas de datos será mínimo.  
  
-   Si la tabla no tiene índice clúster sino uno o más índices no clúster, el registro de las páginas de datos siempre será mínimo. Sin embargo, el modo en que se registran las páginas de índice depende de si la tabla está vacía:  
  
    -   Si la tabla está vacía, el registro de las páginas de índice será mínimo.  
  
    -   Si la tabla no está vacía, el registro de las páginas de índice será completo.  
  
        > [!NOTE]  
        >  Si empieza con una tabla vacía y realiza una importación masiva de datos mediante varios lotes, el registro de las páginas de índice y de datos será mínimo para el primer lote pero, a partir del segundo lote, solo las páginas de datos se registrarán de forma mínima.  
  
-   Si la tabla tiene un índice clúster y está vacía, tanto las páginas de datos como de índice se registrarán de forma mínima. En cambio, si la tabla tiene un índice en clúster basado en btree pero no está vacía, tanto las páginas de datos como las de índice se registrarán de forma completa, independientemente del modelo de recuperación utilizado. Para las tablas con índices de almacén de columnas en clúster, los registros mínimos de los datos cargados en grupos de filas comprimidos siempre se realizan con independencia de que la tabla esté vacía o no cuando el tamaño es igual o superior a 102 400.  
  
    > [!NOTE]  
    >  Si empieza con una tabla de almacén de filas vacía y realiza una importación masiva de datos mediante varios lotes, el registro de las páginas de índice y de datos será mínimo para el primer lote pero, a partir del segundo lote, solo las páginas de datos se registrarán de forma mínima.  
  
> [!NOTE]  
>  Cuando la replicación transaccional está habilitada, las operaciones BULK INSERT se registran por completo en el modelo de recuperación optimizado para cargas masivas de registros.  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Ver o cambiar el modelo de recuperación de una base de datos &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../analysis-services/instances/media/uparrow16x16.png "Icono de flecha usado con el vínculo Volver al principio") [&#91;Principio&#93;](#Top)  
  
## Vea también  
 [Modelos de recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [bcp (utilidad)](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Sugerencias de tabla &#40;Transact-SQL&#41;](../Topic/Table%20Hints%20\(Transact-SQL\).md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)  
  
  