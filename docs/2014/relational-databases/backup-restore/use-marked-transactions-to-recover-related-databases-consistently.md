---
title: Usar transacciones marcadas para recuperar bases de datos relacionadas sistemáticamente (modelo de recuperación completa) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction marks [SQL Server]
- marked transactions [SQL Server]
- database restores [SQL Server], inserting transaction marks for
- recovery [SQL Server], related databases
- restoring databases [SQL Server], related database recovery
- database restores [SQL Server], related databases
- marked transactions [SQL Server], creating
- BEGIN TRAN...WITH MARK statement
- two-phase commit
ms.assetid: 50a73574-1a69-448e-83dd-9abcc7cb7e1a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8dd368ad14f6e521fb8d504bdea774e3088c2522
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84956155"
---
# <a name="use-marked-transactions-to-recover-related-databases-consistently-full-recovery-model"></a>Usar transacciones marcadas para recuperar bases de datos relacionadas sistemáticamente (modelo de recuperación completa)
  Este tema solamente es aplicable a las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usan el modelo de recuperación optimizado para cargas masivas de registros o el modelo de recuperación completa.  
  
 Al realizar actualizaciones relacionadas en dos o más bases de datos, *bases de datos relacionadas*, puede usar marcas de transacción para recuperarlas a un punto con coherencia lógica. Sin embargo, en esta recuperación se pierden todas las transacciones que se confirmaron después de la marca utilizada como punto de recuperación. Las marcas de transacciones solo son adecuadas cuando se están probando bases de datos relacionadas o cuando se está dispuesto a perder las últimas transacciones confirmadas.  
  
 Si se marcan periódicamente las transacciones relacionadas en todas las bases de datos relacionadas, se establece una serie de puntos de recuperación común en las bases de datos. Las marcas de transacción se graban en el registro de transacciones y se incluyen en las copias de seguridad de los registros. Si se produce un desastre, puede restaurar cada una de las bases de datos a la misma marca de transacción para recuperarlas a un punto coherente.  
  
> [!NOTE]  
>  Las copias de seguridad de registros de las distintas bases de datos se pueden crear por separado y no tienen que ser simultáneos.  
  
 La recuperación de bases de datos relacionadas en los escenarios siguientes requiere que ya se hayan marcado las transacciones de todas las bases de datos relacionadas:  
  
-   Uno o más registros de transacciones se destruyen. Tiene que restaurar el conjunto de bases de datos a un estado coherente en el momento de la última copia de seguridad de registros.  
  
-   Tiene que restaurar todo el conjunto de bases de datos a un estado coherente entre sí en algún momento anterior.  
  
> [!IMPORTANT]  
>  Las bases de datos relacionadas solo se pueden recuperar hasta una transacción marcada, no hasta un momento específico.  
  
 Para obtener más información sobre cómo crear transacciones marcadas, vea "Crear las transacciones marcadas" más adelante en este tema.  
  
## <a name="typical-scenario-for-using-marked-transactions"></a>Escenario habitual para utilizar transacciones marcadas  
 Un escenario habitual para usar transacciones marcadas consta de los pasos siguientes:  
  
1.  Crear una copia de seguridad completa o diferencial de cada una de las bases de datos relacionadas.  
  
2.  Marcar un bloque de transacciones en todas las bases de datos.  
  
3.  Realizar una copia de seguridad del registro de transacciones de todas las bases de datos.  
  
4.  Restaurar las copias de seguridad de las bases de datos con WITH NORECOVERY.  
  
5.  Restaurar los registros con WITH STOPATMARK.  
  
## <a name="considerations-for-using-marked-transactions"></a>Consideraciones para el uso de transacciones marcadas  
 Antes de insertar marcas con nombre en el registro de transacciones, tenga en cuenta lo siguiente:  
  
-   Debido a que las marcas de transacción consumen espacio del registro, utilícelas solo para aquellas transacciones que desempeñen un rol importante en la estrategia de recuperación de la base de datos.  
  
-   Después de la confirmación de una transacción marcada, se inserta una fila en la tabla [logmarkhistory](/sql/relational-databases/system-tables/logmarkhistory-transact-sql) de **msdb**.  
  
-   Si la transacción marcada abarca varias bases de datos del mismo servidor de base de datos o de diferentes servidores, las marcas se registran en los registros de todas las bases de datos afectadas.  
  
## <a name="creating-the-marked-transactions"></a>Crear las transacciones marcadas  
 Para crear una transacción marcada, use la instrucción [BEGIN TRANSACTION](/sql/t-sql/language-elements/begin-transaction-transact-sql) y la cláusula WITH MARK [*description*]. La descripción ( *description* ) es opcional y es un texto descriptivo de la marca. Es necesario un nombre de marca para la transacción. Puede volver a usarse un nombre de marca. El registro de transacciones registra el nombre de la marca, su descripción, la base de datos, el usuario, la información de fecha y hora y el número de secuencia de registro (LSN). La información de fecha y hora se utiliza con el nombre de la marca para identificar la marca de forma única.  
  
 **Para crear transacciones marcadas en un conjunto de bases de datos:**  
  
1.  Asigne un nombre a la transacción en la instrucción BEGIN TRAN y use la cláusula WITH MARK.  
  
     Puede anidar la instrucción BEGIN TRAN *new_mark_name* WITH MARK en una transacción existente. El valor de *new_mark_name* es el nombre de marca de la transacción, aunque la transacción tenga un nombre de transacción.  
  
    > [!NOTE]  
    >  Si ejecuta una segunda instrucción anidada BEGIN TRAN...WITH MARK, dicha instrucción se omite pero genera un mensaje de advertencia.  
  
2.  Ejecute una actualización en todas las bases de datos del conjunto.  
  
     La marca de una transacción concreta se inserta en los registros de transacciones solo en la instancia de servidor en que se ejecuta la instrucción BEGIN TRAN...WITH MARK. La marca de transacción se coloca en el registro de transacciones de todas las bases de datos actualizadas por la transacción marcada en esa instancia de servidor. Si las bases de datos se encuentran en distintas instancias de servidor, se deben crear marcas idénticas en cada una de dichas instancias.  
  
### <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se restaura el registro de transacciones hasta la marca de la transacción marcada denominada `ListPriceUpdate`.  
  
```sql  
USE AdventureWorks  
GO  
BEGIN TRANSACTION ListPriceUpdate  
   WITH MARK 'UPDATE Product list prices';  
GO  
  
UPDATE Production.Product  
   SET ListPrice = ListPrice * 1.10  
   WHERE ProductNumber LIKE 'BK-%';  
GO  
  
COMMIT TRANSACTION ListPriceUpdate;  
GO  
  
-- Time passes. Regular database   
-- and log backups are taken.  
-- An error occurs in the database.  
USE master  
GO  
  
RESTORE DATABASE AdventureWorks  
FROM AdventureWorksBackups  
WITH FILE = 3, NORECOVERY;  
GO  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups   
   WITH FILE = 4,  
   RECOVERY,   
   STOPATMARK = 'ListPriceUpdate';  
```  
  
## <a name="forcing-a-mark-to-spread-to-other-servers"></a>Forzar que una marca se distribuya a otros servidores  
 Un nombre de marca de transacción no se distribuye automáticamente a otro servidor cuando se distribuye la transacción. Para forzar que la marca se distribuya a los otros servidores, es necesario escribir un procedimiento almacenado que contenga una instrucción BEGIN TRAN *name* WITH MARK. Ese procedimiento almacenado se debe ejecutar en el servidor remoto en el ámbito de la transacción del servidor de origen.  
  
 Por ejemplo, suponga que hay una base de datos con particiones en varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En cada instancia hay una base de datos cuyo nombre es `coyote`. Primero, cree un procedimiento almacenado, por ejemplo `sp_SetMark`, en todas las bases de datos:  
  
```sql  
CREATE PROCEDURE sp_SetMark  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION @name WITH MARK  
UPDATE coyote.dbo.Marks SET one = 1  
COMMIT TRANSACTION;  
GO  
```  
  
 A continuación, cree el procedimiento almacenado `sp_MarkAll` que contenga una transacción que coloque una marca en cada base de datos. `sp_MarkAll` se puede ejecutar desde cualquiera de las instancias.  
  
```sql  
CREATE PROCEDURE sp_MarkAll  
@name nvarchar (128)  
AS  
BEGIN TRANSACTION  
EXEC instance0.coyote.dbo.sp_SetMark @name  
EXEC instance1.coyote.dbo.sp_SetMark @name  
EXEC instance2.coyote.dbo.sp_SetMark @name  
COMMIT TRANSACTION;  
GO  
```  
  
### <a name="two-phase-commit"></a>confirmación en dos fases  
 La confirmación de una transacción distribuida tiene lugar en dos fases: preparación y confirmación. Cuando se confirma una transacción marcada, la entrada de registro de confirmación de cada base de datos de la transacción marcada se coloca en el registro en un punto en que no hay transacciones dudosas en ninguno de los registros. En este momento, es seguro que ninguna transacción aparecerá como confirmada en un registro pero no en otro.  
  
 Con los siguientes pasos se realiza esta tarea durante la confirmación de una transacción marcada:  
  
1.  La fase de preparación del marcado de una transacción pausa las nuevas operaciones de preparación y confirmación.  
  
2.  Solo podrán continuar las confirmaciones de las transacciones ya preparadas.  
  
3.  A continuación, el marcado de la transacción espera a que terminen todas las transacciones preparadas (con un tiempo de espera).  
  
4.  Se prepara y se confirma la transacción marcada.  
  
5.  Se quita la pausa de las nuevas preparaciones y confirmaciones.  
  
 Las pausas generadas por las transacciones marcadas que abarcan varias bases de datos pueden disminuir el rendimiento del procesamiento de las transacciones del servidor.  
  
 Se recomienda no ejecutar transacciones marcadas a la vez. Aunque es poco frecuente, la confirmación de una transacción marcada distribuida podría interbloquear otras transacciones marcadas distribuidas que se estén confirmando simultáneamente. Si esto sucede, se elegirá el marcado de la transacción como víctima del interbloqueo y se revertirá la operación. Cuando se produce este error, la aplicación puede volver a intentar la transacción marcada. Si se intenta confirmar varias transacciones marcadas simultáneamente, la probabilidad de interbloqueo es mayor.  
  
## <a name="recovering-to-a-marked-transaction"></a>Recuperar a una transacción marcada  
 Para obtener información sobre cómo recuperar una base de datos con transacciones marcadas a una marca concreta o inmediatamente antes, vea [Recuperación de bases de datos relacionadas que contienen transacciones marcadas](recovery-of-related-databases-that-contain-marked-transaction.md).  
  
## <a name="see-also"></a>Consulte también  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/begin-distributed-transaction-transact-sql)   
 [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/begin-transaction-transact-sql)   
 [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [Copias de seguridad completas de bases de datos &#40;SQL Server&#41;](full-database-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Recuperación de bases de datos relacionadas que contienen transacciones marcadas](recovery-of-related-databases-that-contain-marked-transaction.md)  
  
  
