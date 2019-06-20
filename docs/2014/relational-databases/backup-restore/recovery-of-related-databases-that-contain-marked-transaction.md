---
title: Recuperación de bases de datos relacionadas que contienen transacciones marcadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], marks
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- transactions [SQL Server], recovering to a mark
- database recovery [SQL Server]
- marked transactions [SQL Server], restoring
- database restores [SQL Server], point in time
ms.assetid: 77a0d9c0-978a-4891-8b0d-a4256c81c3f8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 209bc81c63998cea299d2c377175955ee99470c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875717"
---
# <a name="recovery-of-related--databases-that-contain-marked-transaction"></a>Recuperación de bases de datos relacionadas que contienen transacciones marcadas
  Este tema solo es pertinente para las bases de datos que contienen transacciones marcadas y utilizan los modelos de recuperación completa u optimizado para cargas masivas de registros.  
  
 Para obtener información sobre los requisitos para la restauración a un punto de recuperación específico, vea [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite insertar marcas con nombre en el registro de transacciones para recuperar hasta esa marca específica. Las marcas del registro son específicas de la transacción y se insertan solo si se confirman sus transacciones asociadas. Como resultado, las marcas se pueden asociar a un trabajo específico y se podrá recuperar hasta un punto que incluya o excluya ese trabajo.  
  
 Antes de insertar marcas con nombre en el registro de transacciones, tenga en cuenta lo siguiente:  
  
-   Debido a que las marcas de transacción consumen espacio del registro, utilícelas solo para aquellas transacciones que desempeñen un rol importante en la estrategia de recuperación de la base de datos.  
  
-   Después de la confirmación de una transacción marcada, se inserta una fila en la tabla [logmarkhistory](/sql/relational-databases/system-tables/logmarkhistory-transact-sql) de **msdb**.  
  
-   Si la transacción marcada abarca varias bases de datos del mismo servidor de base de datos o de diferentes servidores, las marcas se registran en los registros de todas las bases de datos afectadas. Para obtener más información, vea [Usar transacciones marcadas para recuperar bases de datos relacionadas sistemáticamente &#40;modelo de recuperación completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
> [!NOTE]  
>  Para obtener información sobre cómo marcar transacciones, vea [Usar transacciones marcadas para recuperar bases de datos relacionadas sistemáticamente &#40;modelo de recuperación completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="transact-sql-syntax-for-inserting-named-marks-into-a-transaction-log"></a>Sintaxis de Transact-SQL para insertar marcas con nombre en un registro de transacciones  
 Para insertar marcas en los registros de transacciones, use la instrucción [BEGIN TRANSACTION](/sql/t-sql/language-elements/begin-transaction-transact-sql) y la cláusula WITH MARK [*description*]. La marca recibe el mismo nombre que la transacción. La descripción ( *description* ) es opcional y es un texto descriptivo de la marca, no su nombre. Por ejemplo, el nombre de la transacción y de la marca que se crea en la siguiente instrucción `BEGIN TRANSACTION` es `Tx1`:  
  
```wmimof  
BEGIN TRANSACTION Tx1 WITH MARK 'not the mark name, just a description'    
```  
  
 El registro de transacciones registra el nombre de la marca (nombre de la transacción), su descripción, la base de datos, el usuario, la información de `datetime` y el número de flujo de registro (LSN). La información de `datetime` se utiliza con el nombre de la marca para identificar la marca de forma única.  
  
 Para obtener información sobre cómo insertar una marca en una transacción que abarca varias bases de datos, vea [Usar transacciones marcadas para recuperar bases de datos relacionadas sistemáticamente &#40;modelo de recuperación completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
## <a name="transact-sql-syntax-for-recovering-to-a-mark"></a>Sintaxis de Transact-SQL para recuperar hasta una marca  
 Si el destino es una transacción marcada con la instrucción[RESTORE LOG](/sql/t-sql/statements/restore-statements-transact-sql), puede usar una de las cláusulas siguientes para detenerse en la marca o inmediatamente antes:  
  
-   Utilice la cláusula WITH STOPATMARK = **' *`<mark_name>`* '** cláusula para especificar que la transacción marcada es el punto de recuperación.  
  
     STOPATMARK pone al día hasta la marca e incluye la transacción marcada en la puesta al día.  
  
-   Utilice WITH STOPBEFOREMARK = **' *`<mark_name>`* '** cláusula para especificar que el registro que está inmediatamente antes de que la marca es el punto de recuperación.  
  
     STOPBEFOREMARK pone al día hasta la marca y excluye la transacción marcada de la puesta al día.  
  
 Las opciones STOPATMARK y STOPBEFOREMARK admiten una cláusula AFTER *datetime* opcional. Cuando se utiliza *datetime* , no es necesario que los nombres de marca sean únicos.  
  
 Si se omite AFTER *datetime* , la puesta al día se detiene en la primera marca que tenga el nombre especificado. Si se especifica AFTER *datetime* , la puesta al día se detiene en la primera marca que tenga el nombre especificado, ya sea en *datetime*o después.  
  
> [!NOTE]  
>  Al igual que en las operaciones de restauración a un momento dado, la recuperación hasta una marca no está permitida cuando la base de datos está realizando operaciones de registro masivo.  
  
 **Para restaurar una transacción marcada**  
  
 [Restaurar una base de datos en una transacción marcada &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
### <a name="preparing-the-log-backups"></a>Preparar las copias de seguridad de registros  
 En este ejemplo, una estrategia correcta de copia de seguridad para estas bases de datos relacionadas sería:  
  
1.  Utilizar el modelo de recuperación completa para ambas bases de datos.  
  
2.  Crear una copia de seguridad completa de cada base de datos.  
  
     La copia de seguridad de las bases de datos se puede realizar de forma secuencial o simultánea.  
  
3.  Antes de realizar la copia de seguridad del registro de transacciones, marque una transacción que se ejecute en todas las bases de datos. Para obtener información sobre cómo crear transacciones marcadas, vea [Usar transacciones marcadas para recuperar bases de datos relacionadas sistemáticamente &#40;modelo de recuperación completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md).  
  
4.  Realizar una copia de seguridad del registro de transacciones en ambas bases de datos.  
  
### <a name="recovering-the-database-to-a-marked-transaction"></a>Recuperar la base de datos a una transacción marcada  
 **Para restaurar la copia de seguridad**  
  
1.  Cree [copias de seguridad del final del registro](tail-log-backups-sql-server.md) de las bases de datos no dañadas, si es posible.  
  
2.  Restaure la copia de seguridad completa de base de datos más reciente de cada una de las bases de datos.  
  
3.  Identifique la transacción marcada más reciente que esté disponible en todas las copias de seguridad de los registros de transacciones. Esta información se almacena en la tabla **logmarkhistory** de la base de datos **msdb** de cada servidor.  
  
4.  Identifique qué copias de seguridad de registros de todas las bases de datos relacionadas contienen esta marca.  
  
5.  Restaure cada una de las copias de seguridad de registros y deténgase en la transacción marcada.  
  
6.  Recupere cada base de datos.  
  
## <a name="see-also"></a>Vea también  
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/begin-transaction-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Aplicar copias de seguridad de registros de transacción &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [Usar transacciones marcadas para recuperar bases de datos relacionadas sistemáticamente &#40;modelo de recuperación completa&#41;](use-marked-transactions-to-recover-related-databases-consistently.md)   
 [Información general sobre restauración y recuperación &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [Restaurar una base de datos de SQL Server a un momento dado &#40;modelo de recuperación completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Planear y realizar secuencias de restauración &#40;modelo de recuperación completa&#41;](plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
