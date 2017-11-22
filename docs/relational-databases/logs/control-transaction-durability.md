---
title: Control de la durabilidad de las transacciones | Microsoft Docs
ms.custom: 
ms.date: 09/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: logs
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- delayed durability
- Lazy Commit
ms.assetid: 3ac93b28-cac7-483e-a8ab-ac44e1cc1c76
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 469b8008c1697f691c56f6d8893f1d637534c989
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="control-transaction-durability"></a>Controlar la durabilidad de las transacciones
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Las confirmaciones de transacciones de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden ser totalmente durables (el valor predeterminado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) o durables diferidas (conocidas también como confirmaciones diferidas).    
    
 Las confirmaciones de transacciones totalmente durables son sincrónicas y notifican una instrucción COMMIT como correcta para devolver el control al cliente únicamente tras escribir en disco los registros de la transacción. Las confirmaciones de transacciones durables diferidas son asincrónicas y notifican una instrucción COMMIT como correcta antes de escribir en disco los registros de la transacción. Para que una transacción sea durable, es necesario escribir las entradas del registro de transacciones en el disco. Las transacciones durables diferidas pasan a ser durables cuando las entradas del registro de transacciones se vacían en el disco.    
    
 Este tema contiene información detallada sobre las transacciones durables diferidas.    
    
## <a name="full-vs-delayed-transaction-durability"></a>Durabilidad total frente a  durabilidad diferida de transacciones    
 Tanto la durabilidad total como la durabilidad diferida de transacciones tienen sus ventajas y desventajas. Una aplicación puede tener una combinación de transacciones totalmente durables y durables diferidas. Debe considerar detenidamente las necesidades de la empresa y cómo encaja cada una de ellas en esas necesidades.    
    
### <a name="full-transaction-durability"></a>Durabilidad total de transacciones    
 Las transacciones totalmente durables escriben el registro de transacciones en el disco antes de devolver el control al cliente. Debe utilizar transacciones totalmente durables cuando:    
    
-   El sistema no puede tolerar la pérdida de datos.     
    Vea la sección [¿Cuándo puedo perder datos?](../../relational-databases/logs/control-transaction-durability.md#bkmk_DataLoss) para obtener información sobre cuándo puede perder algunos de los datos.    
    
-   El cuello de botella no se debe a la latencia de escritura en el registro de transacciones.    
    
 La durabilidad diferida de transacciones reduce la latencia debida a operaciones de E/S de registro al conservar los registros de transacciones en memoria y escribir por lotes en el registro de transacciones, lo que requiere menos operaciones de E/S. Las transacciones de perdurabilidad diferida reduce potencialmente la contención de las E/S del registro, de forma que se reducen las esperas en el sistema.    
    
 **Garantías de la durabilidad total de transacciones**    
    
-   Una vez que la transacción se confirma correctamente, los cambios que realiza la transacción son visibles para las demás transacciones del sistema. Para obtener más información sobre los niveles de aislamiento de transacciones, vea [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md) o [Transactions with Memory-Optimized Tables (Transacciones con tablas con optimización para memoria)](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md).    
    
-   La durabilidad se garantiza en el momento de la confirmación. Las entradas de registro correspondientes se guardan en el disco antes de que la transacción se confirme correctamente y se devuelva el control al cliente.    
    
### <a name="delayed-transaction-durability"></a>Durabilidad diferida de transacciones    
 La durabilidad diferida de las transacciones se realiza mediante escrituras asincrónicas de registro en el disco. Las entradas del registro de transacciones se conservan en un búfer y se escriben en el disco cuando el búfer se llena o cuando se produce un evento de vaciado del búfer. La durabilidad diferida de las transacciones reduce tanto la latencia como la contención en el sistema porque:    
    
-   El procesamiento de confirmación de transacciones no espera a que finalicen las E/S del registro y a devolver el control al cliente.    
    
-   Resulta menos probable que las transacciones simultáneas compitan por E/S del registro; en su lugar, el búfer de registro puede vaciarse en el disco en fragmentos mayores, lo cual reduce la contención y aumenta el rendimiento.    
    
    > [!NOTE]    
    >  Es posible que siga habiendo contención de E/S si hay un alto grado de simultaneidad, especialmente si el búfer de registro se llena más rápidamente que se vacía.    
    
 #### <a name="when-to-use-delayed-transaction-durability"></a>Cuándo utilizar durabilidad diferida de transacciones    
    
 He aquí algunos casos en los que puede ser beneficioso usar la durabilidad diferida de transacciones:    
    
 **Puede tolerar alguna pérdida de datos.**    
 Si puede tolerar cierta pérdida de datos, por ejemplo cuando los registros individuales no son críticos siempre y cuando tenga la mayoría de los datos, puede resultar útil usar la durabilidad diferida. Si no puede tolerar la pérdida de datos, no utilice la durabilidad diferida de transacciones.    
    
 **Experimenta cuellos de botella en la escritura de registros de transacciones.**    
 Si los problemas de rendimiento se deben a la latencia en la escritura de registros de transacciones, seguramente la aplicación se beneficiará de utilizar la durabilidad diferida de transacciones.    
    
 **Las cargas de trabajo conllevan un alto índice de contención.**    
 Si el sistema tiene cargas de trabajo con un alto índice de contención, se perderá mucho tiempo esperando a que se liberen los bloqueos. La durabilidad diferida de transacciones reduce el tiempo de confirmación y, por tanto, libera los bloqueos con mayor rapidez, lo que redunda en un mayor rendimiento.    
    
 ### <a name="delayed-transaction-durability-guarantees"></a>Garantías de la durabilidad diferida de transacciones   
    
-   Una vez que la transacción se confirma correctamente, los cambios que realiza la transacción son visibles para las demás transacciones del sistema.    
    
-   La durabilidad de las transacciones solo se garantiza después de vaciar en el disco el registro de transacciones en memoria. El registro de transacciones en memoria se vacía en el disco cuando:    
    
    -   Una transacción totalmente durable de la misma base de datos efectúa un cambio en la base de datos y se confirma correctamente.   
    
    -   El usuario ejecuta el procedimiento almacenado del sistema `sp_flush_log` correctamente.     
    
        Si una transacción totalmente durable o sp_flush_log se confirma correctamente, se garantiza que todas las transacciones de durabilidad diferida que se hubieran confirmado anteriormente sean durables.
        
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta vaciar el registro en el disco en función de la generación de registros y del tiempo, incluso si la durabilidad de todas las transacciones es diferida. Esto suele realizarse correctamente si el dispositivo de E/S está al día. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no proporciona garantías de durabilidad sólidas que no sean las transacciones durables y sp_flush_log.      
    
  
    
## <a name="how-to-control-transaction-durability"></a>Cómo controlar la durabilidad de las transacciones    
    
###  <a name="bkmk_DbControl"></a> Control de nivel de base de datos    
 Como administrador de la base de datos (DBA), con la instrucción siguiente puede controlar si los usuarios pueden usar transacciones de durabilidad diferida en una base de datos. Debe establecer la configuración de durabilidad diferida con ALTER DATABASE.    
    
```tsql    
ALTER DATABASE … SET DELAYED_DURABILITY = { DISABLED | ALLOWED | FORCED }    
```    
    
 **DISABLED**    
 [valor predeterminado] Con esta configuración, todas las transacciones que se confirman en la base de datos son totalmente durables, independientemente del nivel de confirmación (DELAYED_DURABILITY= [ON | OFF]). No hay necesidad de modificar y recompilar el procedimiento almacenado. De esta forma, puede asegurarse de que la durabilidad diferida nunca ponga datos en peligro.    
    
 **ALLOWED**    
 Con esta configuración, la durabilidad de cada transacción se determina en el nivel de transacción: DELAYED_DURABILITY = { *OFF* | ON }. Vea [Control de nivel de bloque ATOMIC: procedimientos almacenados compilados de forma nativa](../../relational-databases/logs/control-transaction-durability.md#CompiledProcControl) y [Control de nivel COMMIT: Transact-SQL](../../relational-databases/logs/control-transaction-durability.md#bkmk_T-SQLControl) para obtener más información.    
    
 **FORCED**    
 Con esta configuración, cada transacción que se confirma en la base de datos es durable diferida. Independientemente de que la transacción especifique que es totalmente durable (DELAYED_DURABILITY = OFF) o no haga especificación alguna, la transacción es durable diferida. Esta configuración resulta útil cuando la durabilidad diferida es adecuada para una base de datos y no desea cambiar ningún código de aplicación.    
    
###  <a name="CompiledProcControl"></a> Control de nivel de bloque ATOMIC: procedimientos almacenados compilados de forma nativa    
 El código siguiente va en el interior del bloque ATOMIC.    
    
```tsql    
DELAYED_DURABILITY = { OFF | ON }    
```    
    
 **OFF**    
 [valor predeterminado] La transacción es totalmente durable, salvo que la opción de base de datos DELAYED_DURABLITY = FORCED esté activa, en cuyo caso la instrucción COMMIT será asíncrona y por tanto durable diferida. Consulte [Database level control](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) para obtener más información.    
    
 **ON**    
 La transacción es durable diferida, salvo que la opción de base de datos DELAYED_DURABLITY = DISABLED esté activa, en cuyo caso la instrucción COMMIT será síncrona y por tanto totalmente durable.  Consulte [Database level control](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) para obtener más información.    
    
 **Código de ejemplo**    
    
```tsql    
CREATE PROCEDURE <procedureName> …    
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER    
AS BEGIN ATOMIC WITH     
(    
    DELAYED_DURABILITY = ON,    
    TRANSACTION ISOLATION LEVEL = SNAPSHOT,    
    LANGUAGE = N'English'    
    …    
)    
END    
```    
    
### <a name="table-1-durability-in-atomic-blocks"></a>Tabla 1: durabilidad de bloques ATOMIC    
    
|Opción de durabilidad de bloque ATOMIC|Ninguna transacción existente|Transacción en proceso (totalmente durable o durable diferida)|    
|------------------------------------|-----------------------------|---------------------------------------------------------|    
|**DELAYED_DURABILITY = OFF**|El bloque ATOMIC inicia una nueva transacción totalmente durable.|El bloque ATOMIC crea un punto de retorno en la transacción existente y después inicia la nueva transacción.|    
|**DELAYED_DURABILITY = ON**|El bloque ATOMIC inicia una nueva transacción durable diferida.|El bloque ATOMIC crea un punto de retorno en la transacción existente y después inicia la nueva transacción.|    
    
###  <a name="bkmk_T-SQLControl"></a> Control de nivel COMMIT –[!INCLUDE[tsql](../../includes/tsql-md.md)]    
 La sintaxis de COMMIT se ha ampliado para que pueda forzar la durabilidad diferida de transacciones. Si DELAYED_DURABILITY es DISABLED o FORCED en el nivel de base de datos (vea más arriba), esta opción de COMMIT se omite.    
    
```tsql    
COMMIT [ { TRAN | TRANSACTION } ] [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]    
    
```    
    
 **OFF**    
 [valor predeterminado] La instrucción COMMIT de la transacción es totalmente durable, salvo que la opción de base de datos DELAYED_DURABLITY = FORCED esté activa, en cuyo caso la instrucción COMMIT será asincrónica y por tanto durable diferida. Consulte [Database level control](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) para obtener más información.    
    
 **ON**    
 La instrucción COMMIT de la transacción es durable diferida, salvo que la opción de base de datos DELAYED_DURABLITY = DISABLED esté activa, en cuyo caso la instrucción COMMIT será sincrónica y por tanto totalmente durable. Consulte [Database level control](../../relational-databases/logs/control-transaction-durability.md#bkmk_DbControl) para obtener más información.    
    
### <a name="summary-of-options-and-their-interactions"></a>Resumen de opciones y sus interacciones    
 En esta tabla se resumen las interacciones entre las configuraciones de durabilidad diferida de nivel de base de datos y las configuraciones de nivel de confirmación. Las configuraciones de nivel de base de datos siempre tienen prioridad sobre las configuraciones de nivel de confirmación.    
    
|Valor COMMIT/Valor de base de datos|DELAYED_DURABILITY = DISABLED|DELAYED_DURABILITY = ALLOWED|DELAYED_DURABILITY = FORCED|    
|--------------------------------------|-------------------------------------|------------------------------------|-----------------------------------|    
|**DELAYED_DURABILITY = OFF** Transacciones de nivel de base de datos.|La transacción es totalmente durable.|La transacción es totalmente durable.|La transacción es de durabilidad diferida.|    
|**DELAYED_DURABILITY = ON** Transacciones de nivel de base de datos.|La transacción es totalmente durable.|La transacción es de durabilidad diferida.|La transacción es de durabilidad diferida.|    
|**DELAYED_DURABILITY = OFF** Transacciones entre bases de datos o distribuidas.|La transacción es totalmente durable.|La transacción es totalmente durable.|La transacción es totalmente durable.|    
|**DELAYED_DURABILITY = ON** Transacciones entre bases de datos o distribuidas.|La transacción es totalmente durable.|La transacción es totalmente durable.|La transacción es totalmente durable.|    
    
## <a name="how-to-force-a-transaction-log-flush"></a>Cómo forzar un vaciado del registro de transacciones    
 Existen dos formas de forzar el vaciado en el disco del registro de transacciones.    
    
-   Ejecutar todas las transacciones totalmente durables que modifican la misma base de datos. De esta forma se fuerza un vaciado en disco de las entradas de registro de todas las transacciones de durabilidad diferida confirmadas previamente.    
    
-   Ejecutar el procedimiento almacenado del sistema `sp_flush_log`. Este procedimiento fuerza un vaciado en disco de las entradas de registro de todas las transacciones de durabilidad diferida confirmadas previamente. Para obtener más información, vea [sys.sp_flush_log &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-flush-log-transact-sql.md).    
    
##  <a name="bkmk_OtherSQLFeatures"></a> Durabilidad diferida y otras características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]    
 **Seguimiento de cambios y captura de datos modificados**    
 Todas las transacciones con seguimiento de cambios son totalmente durables. Las transacciones tienen la propiedad de seguimiento de cambios si realizan operaciones de escritura en tablas que se han habilitado para seguimiento de cambios. No se admite el uso de durabilidad diferida para bases de datos que usan captura de datos modificados (CDC).    
    
 **Recuperación tras bloqueo**    
 Se garantiza la coherencia, pero es posible que se pierdan algunas modificaciones de las transacciones de durabilidad diferida que se habían confirmado.    
    
 **Transacciones entre bases de datos y DTC**    
 Si una transacción es entre bases de datos o distribuida, es totalmente durable, independientemente de cualquier configuración de confirmación de base de datos o de transacción.    
    
 **Grupos de disponibilidad AlwaysOn y creación de reflejo**    
 Las transacciones de durabilidad diferida no garantizan la durabilidad del primario ni de los secundarios. Tampoco garantizan ningún conocimiento sobre la transacción en el secundario. Después de COMMIT, se devuelve el control al cliente antes de que se reciba algún reconocimiento desde un elemento secundario sincrónico. La replicación de réplicas secundarias continuará produciéndose mientras tenga lugar el vacío en el disco del primario.   
    
 **Agrupación en clústeres de conmutación por error**    
 Es posible que se pierdan algunas escrituras de transacciones durables diferidas.    
    
 **Replicación de transacciones**    
 Las transacciones durables diferidas no son compatibles con la replicación transaccional.    
    
 **Trasvase de registros**    
 Solo las transacciones que se han convertido en durables se incluyen en el registro que se trasvasa.    
    
 **Copia de seguridad de registros**    
 Solo las transacciones que se han convertido en durables se incluyen en la copia de seguridad.    
    
##  <a name="bkmk_DataLoss"></a> ¿Cuándo puedo perder datos?    
 Si implementa la durabilidad diferida en alguna de las tablas, verá que ciertas condiciones pueden provocar la pérdida de datos. Si no puede tolerar una pérdida de datos, no debería usar la durabilidad diferida en las tablas.    
    
### <a name="catastrophic-events"></a>Catástrofes    
 En caso de catástrofe, como un bloqueo del servidor, perderá los datos de todas las transacciones confirmadas que no se hayan guardado en el disco. Las transacciones de durabilidad diferida se guardan en el disco siempre que se ejecute una transacción totalmente durable respecto a una tabla (optimizada para memoria durable o basada en disco) en la base de datos o cuando se llama a `sp_flush_log` . Si está usando transacciones de durabilidad diferida, conviene crear una tabla pequeña en la base de datos que podrá actualizar regularmente o llamar de forma periódica a `sp_flush_log` para guardar todas las transacciones confirmadas pendientes. El registro de transacciones también se vacía cada vez que se llena, pero es difícil de predecir e imposible de controlar.    
    
### <a name="includessnoversionincludesssnoversion-mdmd-shutdown-and-restart"></a>Cierre y reinicio de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]     
 En lo que respecta a la durabilidad diferida, no hay ninguna diferencia entre el cierre inesperado y el cierre/reinicio planeado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al igual que en las catástrofes, debe prever una pérdida de datos. En un cierre/reinicio planeado, algunas transacciones que no se han escrito en el disco podrían, en primer lugar, guardarse en el disco, pero no debería contar con ello. Tenga previsto sin embargo que en un cierre/reinicio, bien se haya planeado o no, se pierden datos al igual que en las catástrofes.    
    
## <a name="see-also"></a>Vea también    
 [Transacciones con tablas con optimización para memoria](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)    
    
  
