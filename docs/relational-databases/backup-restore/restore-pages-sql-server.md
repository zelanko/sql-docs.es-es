---
title: Restaurar páginas (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: backup-restore
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.restorepage.general.f1
helpviewer_keywords:
- restoring pages [SQL Server]
- pages [SQL Server], restoring
- databases [SQL Server], damaged
- page restores [SQL Server]
- pages [SQL Server], damaged
- restoring [SQL Server], pages
ms.assetid: 07e40950-384e-4d84-9ac5-84da6dd27a91
caps.latest.revision: 67
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d9105a5ac3520514f3998841ca24cf1de7e9a2dc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="restore-pages-sql-server"></a>Restaurar páginas (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo restaurar páginas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. El objetivo de una restauración de páginas es restaurar una o varias páginas dañadas sin restaurar la base de datos completa. Normalmente, las páginas candidatas para la restauración se han marcado como "sospechosas" debido a un error al tener acceso a la página. Las páginas sospechosas se identifican en la tabla [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) de la base de datos **msdb** .  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [¿Cuándo es útil la restauración de páginas?](#WhenUseful)  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para restaurar páginas, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="WhenUseful"></a> ¿Cuándo es útil la restauración de páginas?  
 La restauración de páginas se ha diseñado para reparar páginas aisladas que se han dañado. La restauración y recuperación de una pequeña cantidad de páginas es más rápida que la restauración de un archivo, ya que reduce la cantidad de datos sin conexión durante la operación de restauración. Sin embargo, si debe restaurar una cantidad mayor de páginas de un archivo, la restauración del archivo completo suele ser más efectiva. Por ejemplo, la presencia de un gran número de páginas dañadas en un dispositivo puede indicar un error de dispositivo pendiente. Pruebe a restaurar el archivo, posiblemente en otra ubicación, y repare el dispositivo.  
  
 Además, no todos los errores de página requieren una restauración. Puede producirse un problema en los datos en caché, como por ejemplo un índice secundario, que se puede resolver recalculando los datos. Por ejemplo, si el administrador de base de datos quita un índice secundario y lo vuelve a generar, los datos dañados, aunque se corrijan, no se indican como tales en la tabla [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) .  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   La restauración de páginas se aplica a las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usan los modelos de recuperación optimizado para cargas masivas de registros o completa. La restauración de páginas solo se admite para grupos de archivos de lectura/escritura.  
  
-   Solo se pueden restaurar las páginas de bases de datos. La restauración de páginas no se puede utilizar para restaurar los elementos siguientes:  
  
    -   Registro de transacciones  
  
    -   Páginas de asignación: páginas del mapa de asignación global (GAM), páginas del mapa de asignación global compartido (SGAM) y páginas de espacio disponible en páginas (PFS).  
  
    -   Página 0 de todos los archivos de datos (la página de arranque del archivo)  
  
    -   Página 1:9 (la página de arranque de la base de datos)  
  
    -   Catálogo de texto completo  
  
-   Para una base de datos que utiliza el modelo de recuperación optimizado para cargas masivas de registros, la restauración de páginas cuenta con las condiciones adicionales siguientes:  
  
    -   La realización de copias de seguridad mientras un grupo de archivos o los datos de una página están en modo sin conexión resulta problemática para los datos de registros de operaciones masivas, ya que los datos sin conexión no se encuentran en el registro. La presencia de una página sin conexión puede evitar la realización de una copia de seguridad del registro. En estos casos, intente utilizar DBCC REPAIR, de esta forma la pérdida de datos puede ser menor que si restaura la copia de seguridad más reciente.  
  
    -   Si una copia de seguridad de registros de una base de datos por medio de registros de operaciones masivas detecta una página dañada, se producirá un error a menos que se especifique WITH CONTINUE_AFTER_ERROR.  
  
    -   La restauración de páginas no suele funcionar con la recuperación por medio de registros de operaciones masivas.  
  
         La recomendación para llevar a cabo la restauración de páginas es establecer la base de datos en el modelo de recuperación completa e intentar realizar una copia de seguridad de registros. Si la copia de seguridad de registros funciona, puede pasar a realizar la restauración de páginas. Si la copia de seguridad de registros no se realiza correctamente, perderá el trabajo realizado desde la copia de seguridad de registros anterior o tendrá que intentar ejecutar DBCC con la opción REPAIR_ALLOW_DATA_LOSS.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Escenarios de restauración de páginas:  
  
     Restauración de páginas sin conexión  
     Todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten la restauración de páginas cuando la base de datos está sin conexión. En una restauración de páginas sin conexión, la base de datos está en modo sin conexión mientras se restauran las páginas dañadas. Al final de la secuencia de restauración, la base de datos pasará a estar en línea.  
  
     Restauración de páginas en línea  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition admite restauraciones de páginas en línea, aunque usa la restauración sin conexión si la base de datos está sin conexión en ese momento. En la mayoría de los casos, la restauración de una página dañada se realiza mientras la base de datos, incluido el grupo de archivos para el que la página se restaura, permanece en línea. Cuando el grupo de archivos principal está en línea, aunque alguno de los grupos de archivos secundarios esté sin conexión, las restauraciones de páginas suelen realizarse en línea. Sin embargo, en ocasiones, será necesario utilizar una restauración sin conexión para algunas páginas dañadas. Por ejemplo, cuando los daños en ciertas páginas críticas pueden evitar que se inicie la base de datos.  
  
    > [!WARNING]  
    >  Si las páginas dañadas almacenan metadatos críticos de la base de datos, las actualizaciones necesarias de los metadatos podrían producir un error durante el intento de restauración en línea de las páginas. En este caso, se puede realizar una restauración de páginas sin conexión, pero primero se debe crear una [copia del final del registro](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) (realizando una copia de seguridad del registro de transacciones mediante RESTORE WITH NORECOVERY).  
  
-   La restauración de páginas utiliza el mecanismo mejorado de creación de informes y seguimiento de errores de página (incluidas las sumas de comprobación de página). Las páginas que las sumas de comprobación o las escrituras incompletas detectan como dañadas ( *páginas dañadas*) se pueden restaurar mediante una operación de restauración de páginas. Solo se restauran las páginas que se especifican de forma explícita. Cada página especificada se sustituye por la copia de esa página en la copia de seguridad de datos especificada.  
  
     Cuando se restauran las copias de seguridad de registros posteriores, estas se aplican solo a los archivos de base de datos que contienen al menos una página se está recuperando. Debe aplicarse una cadena ininterrumpida de copias de seguridad de registros a la última recuperación completa o diferencial para actualizar el grupo de archivos que incluye la página al archivo de registro actual. Al igual que en una restauración de archivo, el conjunto de puestas al día se avanza con un solo pase de puesta al día de registro. Para que una restauración de páginas se lleve a cabo correctamente, las páginas restauradas deben recuperarse a un estado coherente con la base de datos.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Si la base de datos que se va a restaurar no existe, el usuario debe tener permisos CREATE DATABASE para poder ejecutar RESTORE. Si la base de datos existe, los permisos RESTORE corresponden de forma predeterminada a los miembros de los roles fijos de servidor **sysadmin** y **dbcreator** , y al propietario (**dbo**) de la base de datos (para la opción FROM DATABASE_SNAPSHOT, la base de datos siempre existe).  
  
 Los permisos RESTORE se conceden a los roles en los que la información acerca de la pertenencia está siempre disponible para el servidor. Debido a que la pertenencia a un rol fijo de base de datos solo se puede comprobar cuando la base de datos es accesible y no está dañada, lo que no siempre ocurre cuando se ejecuta RESTORE, los miembros del rol fijo de base de datos **db_owner** no tienen permisos RESTORE.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 A partir de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] admite las restauraciones de páginas.  
  
#### <a name="to-restore-pages"></a>Para restaurar páginas  
  
1.  Conéctese a la instancia adecuada del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, en el Explorador de objetos, haga clic en el nombre del servidor para expandir el árbol.  
  
2.  Expanda **Bases de datos**. En función de la base de datos, seleccione una base de datos de usuario o expanda **Bases de datos del sistema**y, a continuación, seleccione una base de datos del sistema.  
  
3.  Haga clic con el botón derecho en la base de datos, seleccione **Tareas**, seleccione **Restaurar**y haga clic en **Página**, con lo que se abre el cuadro de diálogo **Restaurar página** .  
  
     **Restauración**  
     En esta sección se realiza la misma función que la de **Restaurar en** en [Restaurar base de datos (página General)](../../relational-databases/backup-restore/restore-database-general-page.md).  
  
     **Base de datos**  
     Especifica la base de datos que se va a restaurar. Puede especificar una base de datos nueva o seleccionar una base de datos existente de la lista desplegable. La lista incluye todas las bases de datos del servidor, excepto las bases de datos del sistema **maestra** y **tempdb**.  
  
    > [!WARNING]  
    >  Para restaurar una copia de seguridad protegida con contraseña, use la instrucción [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) .  
  
     **Copia del final del registro**  
     Escriba o seleccione un nombre de archivo en **Dispositivo de copia de seguridad** , en el que la copia del final del registro se almacenará en la base de datos.  
  
     **Conjuntos de copia de seguridad**  
     Esta sección muestra los conjuntos de copia de seguridad implicados en la restauración.  
  
    |Encabezado|Valores|  
    |------------|------------|  
    |**Nombre**|Nombre del conjunto de copia de seguridad.|  
    |**Componente**|Componente del que se ha realizado una copia de seguridad: **Base de datos**, **Archivo** o **\<en blanco>** (para registros de transacciones).|  
    |**Tipo**|Tipo de copia de seguridad realizada: **Completa**, **Diferencial**o **Registro de transacciones**.|  
    |**Server**|Nombre de la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] que realizó la operación de copia de seguridad.|  
    |**Base de datos**|Nombre de la base de datos para la operación de copia de seguridad.|  
    |**Posición**|Posición del conjunto de copias de seguridad en el volumen.|  
    |**Primer LSN**|Número de secuencia de registro (LSN) de la primera transacción del conjunto de copias de seguridad. En blanco para las copias de seguridad de archivos.|  
    |**Último LSN**|Número de secuencia de registro (LSN) de la última transacción del conjunto de copias de seguridad. En blanco para las copias de seguridad de archivos.|  
    |**LSN de punto de comprobación**|Número de secuencia de registro (LSN) del punto de comprobación más reciente en el momento en que se creó la copia de seguridad.|  
    |**LSN completo**|Número de secuencia de registro (LSN) de la copia de seguridad completa más reciente de la base de datos.|  
    |**Fecha de inicio**|Fecha y hora en la que se inició la operación de copia de seguridad, presentadas en la configuración regional del cliente.|  
    |**Fecha final**|Fecha y hora en la que finalizó la operación de copia de seguridad, presentadas en la configuración regional del cliente.|  
    |**Tamaño**|Tamaño del conjunto de copias de seguridad, en bytes.|  
    |**Nombre de usuario**|Nombre del usuario que realizó la operación de copia de seguridad.|  
    |**Expiración**|Fecha y hora de expiración del conjunto de copias de seguridad.|  
  
     Haga clic en **Comprobar** para comprobar la integridad de los archivos de copia de seguridad necesarios para realizar la operación de restauración de páginas.  
  
4.  Para identificar las páginas dañadas, con la base de datos correcta seleccionado en el cuadro **Base de datos** , haga clic en **Comprobar páginas de la base de datos**. Se trata de una operación de ejecución prolongada.  
  
    > [!WARNING]  
    >  Para restaurar páginas específicas que no están dañadas, haga clic en **Agregar** y escriba el **Id. de archivo** y el **Id. de página** de las páginas que se van a restaurar.  
  
5.  La cuadrícula de páginas se utiliza para identificar las páginas que se van a restaurar. Inicialmente, esta cuadrícula se rellena desde la tabla del sistema [suspect_pages](../../relational-databases/system-tables/suspect-pages-transact-sql.md) . Para agregar o quitar páginas en la cuadrícula, haga clic en **Agregar** o en **Quitar**. Para obtener más información, vea [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md).  
  
6.  La cuadrícula **Conjuntos de copia de seguridad** muestra una lista de los conjuntos de copia de seguridad en el plan de restauración predeterminado. Opcionalmente, haga clic en **Comprobar** para comprobar que las copias de seguridad son legibles y que los conjuntos de copia de seguridad están completos, sin restaurarlos. Para obtener más información, vea [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md).  
  
     **Páginas**  
  
7.  Para restaurar las páginas incluidas en la cuadrícula de páginas, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Para especificar una página en una instrucción RESTORE DATABASE, necesita el identificador de archivo del archivo que contiene la página y el identificador de la página. La sintaxis necesaria es la siguiente:  
  
 `RESTORE DATABASE <database_name>`  
  
 `PAGE = '<file: page> [ ,... n ] ' [ ,... n ]`  
  
 `FROM <backup_device> [ ,... n ]`  
  
 `WITH NORECOVERY`  
  
 Para obtener más información sobre los parámetros de la opción PAGE, vea [Argumentos RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md). Para obtener más información sobre la sintaxis de RESTORE DATABASE, vea [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md).  
  
#### <a name="to-restore-pages"></a>Para restaurar páginas  
  
1.  Obtener los Id. de las páginas dañadas que se deben restaurar. Un error de suma de comprobación o escritura incompleta devuelve el Id. de página con la información necesaria para especificar las páginas. Para buscar el identificador de una página dañada, use cualquiera de los siguientes orígenes.  
  
    |Origen de identificador de página|Tema|  
    |-----------------------|-----------|  
    |**msdb..suspect_pages**|[Administrar la tabla suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)|  
    |Registro de errores|[Ver el registro de errores de SQL Server &#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)|  
    |Seguimientos de eventos|[Supervisar y responder a eventos](http://msdn.microsoft.com/library/f7fbe155-5b68-4777-bc71-a47637471f32)|  
    |DBCC|[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)|  
    |Proveedor WMI|[Conceptos del proveedor WMI para eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)|  
  
2.  Iniciar una restauración de páginas con una copia de seguridad completa de base de datos, de archivo o de grupo de archivos que contenga la página. En la instrucción RESTORE DATABASE, utilice la cláusula PAGE para obtener los Id. de todas las páginas que se deben restaurar.  
  
3.  Aplicar las copias de seguridad diferenciales más recientes.  
  
4.  Aplicar las copias de seguridad de registros posteriores.  
  
5.  Crear una nueva copia de seguridad de registros de la base de datos que incluya el LSN final de las páginas restauradas; es decir, el punto en que la última página restaurada ha pasado a estar en modo sin conexión. El LSN final, que se establece como parte de la primera restauración de la secuencia, es el LSN final de puesta al día. La puesta al día en línea del archivo que contiene la página puede detenerse en el LSN final de puesta al día. Para conocer el LSN actual de destino de fase de puesta al día de un archivo, vea la columna **redo_target_lsn** de **sys.master_files**. Para obtener más información, vea [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md).  
  
6.  Restaurar la copia de seguridad de registros nueva. Después de aplicar esta nueva copia de seguridad de registros, la restauración de páginas finaliza y las páginas están listas para su uso.  
  
    > [!NOTE]  
    >  Esta secuencia es análoga a una secuencia de restauración de archivos. De hecho, tanto la restauración de páginas como la de archivos puede realizarse como parte de la misma secuencia.  
  
###  <a name="TsqlExample"></a> Ejemplo (Transact-SQL)  
 En el siguiente ejemplo se restauran cuatro páginas dañadas del archivo `B` con `NORECOVERY`. A continuación, se aplican dos copias de seguridad de registros con `NORECOVERY`y, después, la copia del final del registro, restaurada con `RECOVERY`. En este ejemplo se realiza una restauración en línea. En el ejemplo, el identificador del archivo `B` es `1`y los identificadores de las páginas dañadas son `57`, `202`, `916`y `1016`.  
  
```sql  
RESTORE DATABASE <database> PAGE='1:57, 1:202, 1:916, 1:1016'  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;   
BACKUP LOG <database> TO <new_log_backup>;   
RESTORE LOG <database> FROM <new_log_backup> WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [Administrar la tabla suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)   
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
