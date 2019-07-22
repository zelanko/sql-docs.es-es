---
title: Restauraciones por etapas (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- partial updates [SQL Server]
- staged restores [SQL Server]
- piecemeal restores [SQL Server]
- restoring [SQL Server], piecemeal restore scenario
ms.assetid: 208f55e0-0762-4cfb-85c4-d36a76ea0f5b
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8dfdfc8ea7d34975046545688cca3f34ed324311
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033652"
---
# <a name="piecemeal-restores-sql-server"></a>Restauraciones por etapas (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tema se aplica a las bases de datos de la edición Enterprise de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (restauración con conexión) o de la edición Estándar (restauración sin conexión) que incluyan varios archivos o grupos de archivos y, en el modelo simple, únicamente para grupos de archivos de solo lectura.  
  
 Para obtener información sobre la restauración por etapas y las tablas optimizadas para memoria, vea [Restauración por etapas de bases de datos con tablas optimizadas para memoria](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md).  
  
 La*restauración por etapas* , permite la restauración y recuperación en fases de las bases de datos que contienen varios grupos de archivos. Este tipo de restauración implica una serie de secuencias de restauración, empezando por el grupo de archivos principal y, en algunos casos, uno o varios grupos de archivos secundarios. La restauración por etapas mantiene comprobaciones para garantizar que, al final, la base de datos será coherente. Una vez completada la secuencia de restauración, los archivos recuperados (si son válidos y coherentes con la base de datos) pueden ponerse en línea directamente.  
  
 La restauración por etapas funciona con todos los modelos de recuperación, pero su flexibilidad es mayor para los modelos de recuperación optimizado para cargas masivas de registros y completo que para el modelo de recuperación simple.  
  
 Las restauraciones por etapas empiezan con una secuencia de restauración inicial que se denomina *secuencia de restauración parcial*. Como mínimo, la secuencia de restauración parcial restaura y recupera el grupo de archivos principal y, con el modelo de recuperación simple, todos los grupos de archivos de lectura/escritura. Durante la secuencia de restauración por etapas, toda la base de datos debe ponerse en modo sin conexión. Después de este momento, la base de datos estará en línea y los grupos de archivos restaurados estarán disponibles. Sin embargo, los grupos de archivos no restaurados permanecerán sin conexión y no estarán disponibles. No obstante, los grupos de archivos sin conexión se pueden restaurar y poner en línea más adelante mediante una restauración de archivos.  
  
 Independientemente del modelo de recuperación utilizado por la base de datos, la secuencia de restauración parcial se inicia con una instrucción RESTORE DATABASE que restaura una copia de seguridad completa y especifica la opción PARTIAL. La opción PARTIAL siempre inicia una nueva restauración por etapas; por lo tanto, se debe especificar PARTIAL únicamente una vez en la instrucción inicial de la secuencia de restauración parcial. Cuando la secuencia de restauración parcial finaliza y la base de datos está en línea, a los archivos restantes se les asigna el estado "pendiente de recuperación" porque su recuperación se ha pospuesto.  
  
 Posteriormente, una restauración por etapas suele incluir una o varias secuencias de restauración, que se denominan *secuencias de restauración de grupos de archivos*. Se puede retrasar la realización de una secuencia de restauración de grupos de archivos concreta el tiempo que desee. Estas secuencias restauran y recuperan uno o varios grupos de archivos sin conexión a un punto coherente con la base de datos. La planeación y el número de secuencias de restauración de grupos de archivos depende del objetivo de recuperación, del número de grupos de archivos sin conexión que se desea restaurar y de cuántos de estos se restaurarán por secuencia de restauración de grupos de archivos.  
  
 Los requisitos concretos para realizar una restauración por etapas dependen del modelo de recuperación de la base de datos. Para obtener información, vea "	Restauración por etapas con el modelo de recuperación simple" y "Restauración por etapas con el modelo de recuperación completa", más adelante en este tema.  
  
## <a name="piecemeal-restore-scenarios"></a>Escenarios de restauración por etapas  
 Todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten restauraciones por etapas sin conexión. En la edición Enterprise, una restauración por etapas puede realizarse en línea o sin conexión. Las implicaciones de las restauraciones por etapas en línea y sin conexión son las siguientes:  
  
-   Escenario de restauración por etapas sin conexión  
  
     En una restauración por etapas sin conexión, la base de datos está en línea después de la secuencia de restauración parcial. Los grupos de archivos que aún no se han restaurado permanecen sin conexión, pero pueden restaurarse a medida que sean necesarios después de dejar la base de datos sin conexión.  
  
-   Escenario de restauración por etapas en línea  
  
     En una restauración por etapas en línea, tras secuencia de restauración parcial, la base de datos está en línea y el grupo de archivos principal y los grupos de archivos secundarios recuperados están disponibles. Los grupos de archivos que todavía no se han restaurado permanecen sin conexión, pero se pueden restaurar cuando sea necesario mientras la base de datos se encuentre en línea.  
  
     Las restauraciones por etapas en línea pueden incluir transacciones diferidas. Cuando solo se restaura un subconjunto de grupos de archivos, puede que se difieran las transacciones de la base de datos que dependan de los grupos de archivos en línea. Esto es normal, porque toda la base de datos debe ser coherente. Para obtener más información, vea [Transacciones diferidas &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md).  
  
-   [!INCLUDE[hek_1](../../includes/hek-1-md.md)] escenario de restauración por etapas  
  
     Para obtener información sobre las restauraciones por etapas de bases de datos de OLTP en memoria, vea [Copias de seguridad y restauración por etapas de bases de datos con tablas con optimización para memoria](../../relational-databases/in-memory-oltp/piecemeal-restore-of-databases-with-memory-optimized-tables.md).  
  
## <a name="restrictions"></a>Restrictions  
 Si una secuencia de restauración parcial excluye cualquier grupo de archivos [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md) , no se admite la restauración a un momento dado. Puede forzarse la continuación de la secuencia de restauración. Sin embargo, no se podrán restaurar los grupos de archivos FILESTREAM omitidos en la instrucción RESTORE. Para forzar una restauración a un momento específico, especifique la opción CONTINUE_AFTER_ERROR junto con la opción STOPAT, STOPATMARK o STOPBEFOREMARK, que debe especificar también en las instrucciones RESTORE LOG siguientes. Si se especifica CONTINUE_AFTER_ERROR, la secuencia de restauración parcial será correcta y el grupo de archivos FILESTREAM no será recuperable.  
  
## <a name="piecemeal-restore-under-the-simple-recovery-model"></a>Restauración por etapas con el modelo de recuperación simple  
 Con el modelo de recuperación simple, la secuencia de restauración por etapas debe comenzar con una copia de seguridad completa o parcial de la base de datos. A continuación, si la copia de seguridad restaurada es una base diferencial, restaure la copia de seguridad diferencial más reciente.  
  
 Durante la primera secuencia de restauración parcial, si solo se restaura un subconjunto de grupos de archivos de lectura/escritura, todos los grupos de archivos no restaurados quedan inactivos al recuperar la base de datos restaurada parcialmente. La exclusión de un grupo de archivos de lectura/escritura de una secuencia de restauración parcial solo es apropiada en los siguientes casos:  
  
-   Desea que los grupos de archivos no restaurados queden inactivos.  
  
-   La secuencia de restauración alcanzará un punto de recuperación en el que cada grupo de archivos no restaurado ha pasado a ser de solo lectura, se ha eliminada o ha quedado inactivo (durante una restauración anterior de la secuencia de restauración parcial).  
  
-   La copia de seguridad completa se realizó mientras la base de datos utilizaba el modelo de recuperación simple, pero el punto de recuperación es de un momento cuando la base de datos utilizaba el modelo de recuperación completa. Para obtener información, vea "Realizar una restauración por etapas de una base de datos cuyo modelo de recuperación ha cambiado de simple a completo", más adelante en este tema.  
  
### <a name="requirements-for-piecemeal-restore-under-the-simple-recovery-model"></a>Requisitos de la restauración por etapas con el modelo de recuperación simple  
 Con el modelo de recuperación simple, la fase inicial restaura y recupera el grupo de archivos principal y todos los grupos de archivos de lectura/escritura secundarios. Una vez terminada la fase inicial, los archivos recuperados (si son válidos y coherentes con la base de datos) pueden ponerse en línea directamente.  
  
 A partir de ese momento, se pueden restaurar los grupos de archivos de solo lectura en una o varias fases adicionales.  
  
 La restauración por etapas está disponible para un grupo de archivos secundarios de solo lectura únicamente si se cumple lo siguiente:  
  
-   Era de solo lectura cuando se hizo su copia de seguridad.  
  
-   Ha permanecido como solo lectura (y se mantiene la coherencia lógica con el grupo de archivos principal).  
  
 Para realizar una restauración por etapas, se deben seguir estas directrices:  
  
-   Un conjunto de copias de seguridad completo para la restauración por etapas de una base de datos con el modelo de recuperación simple debe contener lo siguiente:  
  
    -   Una copia de seguridad de base de datos parcial o completa que contenga el grupo de archivos principal y todos los grupos de archivos que tenían acceso de lectura/escritura al hacer la copia de seguridad.  
  
    -   Una copia de seguridad de cada archivo de solo lectura.  
  
-   Para que la copia de seguridad de un archivo de solo lectura sea coherente con el grupo de archivos principal, el grupo de archivos secundario debe haber sido de solo lectura desde que se hizo la copia de seguridad hasta que se completó la copia de seguridad que incluye el grupo de archivos principal. Puede usar copias de seguridad diferenciales de archivos si se hicieron después de que el grupo de archivos pasara a ser de solo lectura.  
  
### <a name="piecemeal-restore-stages-simple-recovery-model"></a>Fases de la restauración por etapas (modelo de recuperación simple)  
 El escenario de restauración por etapas implica las siguientes etapas:  
  
-   Fase inicial (restauración y recuperación del grupo de archivos principal y de todos los grupos de archivos de lectura/escritura)  
  
     La etapa inicial realiza una restauración parcial. La secuencia de restauración parcial restaura el grupo de archivos principal, todos los grupos de archivos secundarios de lectura/escritura y, opcionalmente, algunos grupos de archivos de solo lectura. Durante la fase inicial, toda la base de datos debe pasar a modo sin conexión. Después de la etapa inicial, la base de datos está en línea y los grupos de archivos restaurados estarán disponibles. Sin embargo, los grupos de archivos de solo lectura que aún no se han restaurado permanecen sin conexión.  
  
     La primera instrucción RESTORE de la fase inicial debe realizar lo siguiente:  
  
    -   Usar una copia de seguridad parcial o completa de la base de datos que incluya el grupo de archivos principal y todos los grupos de archivos que eran de lectura/escritura al hacer la copia de seguridad. Es normal comenzar una secuencia de restauración parcial mediante la restauración de una copia de seguridad parcial.  
  
    -   Especificar la opción PARTIAL, que indica el inicio de una restauración por etapas.  
  
    > [!NOTE]  
    >  La opción PARTIAL realiza comprobaciones de seguridad que garantizan que la base de datos resultante es adecuada para su uso como base de datos de producción.  
  
    -   Especificar la opción READ_WRITE_FILEGROUPS si la copia de seguridad es una copia de seguridad de base de datos completa.  
  
-   Mientras la base de datos esté en línea, se pueden usar una o varias restauraciones de archivos en línea para restaurar y recuperar archivos de solo lectura sin conexión que eran de solo lectura cuando se realizó la copia de seguridad. La programación de la restauración de archivos en línea depende de cuándo desee que los datos tengan conexión.  
  
     La restauración de los datos a un archivo depende de lo siguiente:  
  
    -   Los archivos válidos de solo lectura que son coherentes con la base de datos pueden ponerse en línea directamente si se recuperan sin restaurar ningún dato.  
  
    -   Los archivos dañados o incoherentes con la base de datos se deben restaurar antes de recuperarlos.  
  
### <a name="examples"></a>Ejemplos  
  
-   [Ejemplo: restauración por etapas de la base de datos &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación simple&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="piecemeal-restore-under-the-full-recovery-model"></a>Restauración por etapas con el modelo de recuperación completa  
 Con el modelo de recuperación completa o el modelo de recuperación optimizado para cargas masivas de registros, se puede realizar una restauración por etapas de cualquier base de datos que incluya varios grupos de archivos y se puede restaurar una base de datos a cualquier momento dado en el tiempo. Las secuencias de la restauración por etapas son las siguientes:  
  
-   secuencia de restauración parcial  
  
     La secuencia de restauración parcial restaura el grupo de archivos principal y, opcionalmente, algunos de los grupos de archivos secundarios.  
  
     La primera instrucción RESTORE DATABASE debe realizar lo siguiente:  
  
    -   Especificar la opción PARTIAL, que indica el inicio de una restauración por etapas.  
  
    -   Utilizar cualquier copia de seguridad completa que contenga el grupo de archivos principal. La práctica normal es comenzar una secuencia de restauración parcial mediante la restauración de una copia de seguridad parcial.  
  
    -   Para restaurar a un momento específico, se debe especificar este momento en la secuencia de restauración parcial. Las fases sucesivas de la secuencia de restauración deberán especificar el mismo momento.  
  
-   Las secuencias de restauración de grupos de archivos ponen en línea los grupos de archivos adicionales en un punto coherente con la base de datos.  
  
     En la edición Enterprise, se puede restaurar y recuperar cualquier grupo de archivos secundario sin conexión mientras la base de datos permanece en línea. Si un determinado archivo de solo lectura está dañado o no es coherente con la base de datos, no necesita restauración. Para obtener más información, vea [Recuperar una base de datos sin restaurar los datos &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md).  
  
### <a name="applying-log-backups"></a>Aplicar copias de seguridad de registros  
 Si un grupo de archivos de solo lectura ha sido de solo lectura desde antes de la creación de la copia de seguridad de archivos, no es necesario aplicar las copias de seguridad de registros al grupo de archivos y éstas se omiten en la restauración de archivos. Si el grupo de archivos es de lectura/escritura, debe aplicarse una cadena ininterrumpida de copias de seguridad de registros a la última recuperación completa o diferencial para actualizar el grupo de archivos al archivo de registro actual.  
  
### <a name="examples"></a>Ejemplos  
  
-   [Ejemplo: restauración por etapas de la base de datos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Ejemplo: restauración por etapas exclusiva para algunos grupos de archivos &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
## <a name="performing-a-piecemeal-restore-of-a-database-whose-recovery-model-has-been-switched-from-simple-to-full"></a>Realizar una restauración por etapas de una base de datos cuyo modelo de recuperación ha cambiado de simple a completo  
 Puede realizar una restauración por etapas de una base de datos cuyo modelo de recuperación haya cambiado de un modelo de recuperación simple a uno completo desde la creación de la copia de seguridad parcial, completa o de base de datos. Por ejemplo, supongamos que realiza los siguientes pasos para una base de datos:  
  
1.  Crea una copia de seguridad parcial (copia_1) de una base de datos de modelo simple.  
  
2.  Al cabo de un tiempo, cambia el modelo de recuperación a completo.  
  
3.  Crea una copia de seguridad diferencial.  
  
4.  Comienza a realizar copias de seguridad de registros.  
  
 A partir de este punto, la siguiente secuencia será válida:  
  
1.  Una restauración parcial que omite algunos grupos de archivos secundarios.  
  
2.  Una restauración diferencial seguida de otras restauraciones necesarias.  
  
3.  Más adelante, una restauración de un grupo de archivos secundarios de lectura/escritura con WITH NORECOVERY de la copia de seguridad parcial copia_1.  
  
4.  Una copia de seguridad diferencial se realiza después de otras copias de seguridad restauradas en la secuencia de restauración por etapas original para restaurar los datos hasta el punto de recuperación original.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="see-also"></a>Consulte también  
 [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [Planear y realizar secuencias de restauración &#40;modelo de recuperación completa&#41;](../../relational-databases/backup-restore/plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
