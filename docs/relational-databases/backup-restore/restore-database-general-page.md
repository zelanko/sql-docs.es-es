---
title: Restaurar la base de datos (página General) | Microsoft Docs
ms.custom: ''
ms.date: 07/01/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoredb.general.f1
ms.assetid: 160cf58c-b06a-475f-9a69-2b051e5767ab
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 050fb8ed2364066dfe0a6a41e41ec295590d7895
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155517"
---
# <a name="restore-database-general-page"></a>Restaurar la base de datos (página General)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use la página **General** para especificar información sobre las bases de datos de destino y de origen para una operación de restauración de base de datos.  
    
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  Cuando especifica una tarea de restauración mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede generar el script [!INCLUDE[tsql](../../includes/tsql-md.md)] [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) correspondiente si hace clic en **Script** y luego selecciona un destino para el script.  
  
## <a name="permissions"></a>Permisos  
 Si la base de datos que se va a restaurar no existe, el usuario debe tener permisos CREATE DATABASE para poder ejecutar RESTORE. Si la base de datos existe, los permisos RESTORE corresponden de forma predeterminada a los miembros de los roles fijos de servidor **sysadmin** y **dbcreator** , y al propietario (**dbo**) de la base de datos.  
  
 Los permisos RESTORE se conceden a los roles en los que la información acerca de la pertenencia está siempre disponible para el servidor. Debido a que la pertenencia a un rol fijo de base de datos solo se puede comprobar cuando la base de datos es accesible y no está dañada, lo que no siempre ocurre cuando se ejecuta RESTORE, los miembros del rol fijo de base de datos **db_owner** no tienen permisos RESTORE.  
  
 La restauración de una copia de seguridad cifrada requiere permisos **VIEW DEFINITION** al certificado o a la clave asimétrica que se usó para el cifrado durante la copia de seguridad.  
  
## <a name="options"></a>Opciones  
  
### <a name="source"></a>Source  
 Las opciones del panel **Restore from**(Restaurar desde) identifican la ubicación de los conjuntos de copia de seguridad para la base de datos y los conjuntos de copia de seguridad que quiere restaurar.  
  
|Término|Definición|  
|----------|----------------|  
|**Base de datos**|Seleccione la base de datos que desea restaurar en la lista desplegable. La lista solo contiene las bases de datos de las que se han realizado copias de seguridad de acuerdo con el historial de copias de seguridad de **msdb** .|  
|**Dispositivo**|Seleccione los dispositivos de copia de seguridad lógicos o físicos (cintas, direcciones URL o archivos) que contienen las copias de seguridad que desee restaurar. Es obligatorio si la copia de seguridad de la base de datos se realizó de otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para seleccionar uno o varios dispositivos de copia de seguridad lógicos o físicos, haga clic en el botón Examinar, que abre el cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** . En dicho cuadro, puede seleccionar hasta 64 dispositivos pertenecientes a un conjunto de medios. Los dispositivos de cinta deben estar conectados físicamente al equipo donde se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un archivo de copia de seguridad puede estar en un dispositivo de disco local o extraíble. Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md). También puede seleccionar **Dirección URL** como el tipo de dispositivo de copia de seguridad almacenado en Azure Storage.<br /><br /> Al salir del cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** , el dispositivo seleccionado aparecerá en forma de valores de solo lectura en la lista **Dispositivo** .|  
|**Base de datos**|Seleccione el nombre de la base de datos cuyas copias de seguridad se deben restaurar en el cuadro de lista desplegable.<br /><br /> Nota: Esta lista solo está disponible cuando se selecciona la opción **Dispositivo** . Solo estarán disponibles las bases de datos que tienen copias de seguridad en los dispositivos seleccionados.|  
  
### <a name="destination"></a>Destino  
 Las opciones del panel **Restaurar en** identifican la base de datos y el punto de restauración.  
  
|Término|Definición|  
|----------|----------------|  
|**Base de datos**|Especifique la base de datos de la lista que debe restaurarse. Puede especificar una nueva base de datos o elegir una base de datos existente de la lista desplegable. La lista incluye todas las bases de datos del servidor, y excluye las bases de datos del sistema **master** y **tempdb**.<br /><br /> Nota: Para restaurar una copia de seguridad protegida con contraseña, use la instrucción [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) .|  
|**Restaurar en**|El cuadro **Restaurar en** se establecerá en "A la última copia de seguridad realizada" de forma predeterminada. También puede hacer clic en **Escala de tiempo** para que se muestre el cuadro de diálogo **Escala de tiempo de la copia de seguridad** , que muestra el historial de copias de seguridad de la base de datos en forma de escala de tiempo. Haga clic en **Escala de tiempo** para designar un valor de **datetime** específico para el que desea restaurar la base de datos. La base de datos se restaurará al estado en que estaba en este momento especificado. Consulte [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md).|  
  
### <a name="restore-plan"></a>Plan de restauraciones  
  
|Término|Definición|Valores|  
|----------|----------------|------------|  
|**Conjuntos de copia de seguridad para restaurar**|Muestra los conjuntos de copia de seguridad disponibles para la ubicación especificada. Cada conjunto de copia de seguridad, resultado de una sola operación de copia de seguridad, se distribuye entre todos los dispositivos del conjunto de medios. De forma predeterminada, se sugiere un plan de recuperación para alcanzar el objetivo la operación de restauración según la selección de los conjuntos de copia de seguridad necesarios. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa el historial de copias de seguridad de **msdb** para identificar las copias de seguridad que son necesarias para restaurar una base de datos y crea un plan de restauración. Por ejemplo, para la restauración de una base de datos, el plan de restauración selecciona la copia de seguridad completa más reciente de la base de datos y la siguiente copia de seguridad diferencial más reciente de la base de datos, si ésta existiese. Con el modelo de recuperación completa, el plan de restauración selecciona, a continuación, todas las copias de seguridad de registros siguientes.<br /><br /> Para anular el plan de recuperación sugerido, puede cambiar las selecciones de la cuadrícula. Se anulará automáticamente la selección de aquellas copias de seguridad que dependan de una copia de seguridad cuya selección fue anulada.<br /><br /> Las casillas se habilitan solo cuando se activa la casilla **Selección manual** . Esto permite seleccionar los conjuntos de copia de seguridad que deben restaurarse.<br /><br /> Cuando se activa la casilla **Selección manual** , la precisión del plan de restauraciones se comprueba cada vez que se modifica. Si la secuencia de copias de seguridad es incorrecta, aparecerá un mensaje de error.|**Restauración**: <br />                          Las casillas activadas indican los conjuntos de copias de seguridad que se restaurarán.<br /><br /> **Nombre**: <br />                          Nombre del conjunto de copia de seguridad.<br /><br /> **Componente**: Componente del que se ha realizado una copia de seguridad: **Base de datos**, **Archivo** o **\<en blanco>** (para registros de transacciones).<br /><br /> **Tipo**: Tipo de copia de seguridad realizada: **Completa**, **Diferencial** o **Registro de transacciones**.<br /><br /> **Servidor**: Nombre de la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] que realizó la operación de copia de seguridad.<br /><br /> **Base de datos**: <br />                          Nombre de la base de datos para la operación de copia de seguridad.<br /><br /> **Posición**: Posición del conjunto de copias de seguridad en el volumen.<br /><br /> **Primer LSN**: <br />                          Número de secuencia de registro de la primera transacción del conjunto de copias de seguridad. En blanco para las copias de seguridad de archivos.<br /><br /> **Último LSN**: <br />                          Número de secuencia de registro de la última transacción del conjunto de copias de seguridad. En blanco para las copias de seguridad de archivos.<br /><br /> **LSN de punto de comprobación**: <br />                          Número de secuencia de registro (LSN) del punto de comprobación más reciente en el momento en que se creó la copia de seguridad.<br /><br /> **LSN completo**: <br />                          Número de secuencia de registro de la copia de seguridad completa más reciente de la base de datos.<br /><br /> **Fecha de inicio**: <br />                          Fecha y hora en la que se inició la operación de copia de seguridad, presentadas en la configuración regional del cliente.<br /><br /> **Fecha final**: <br />                          Fecha y hora en la que finalizó la operación de copia de seguridad, presentadas en la configuración regional del cliente.<br /><br /> **Tamaño**: <br />                          Tamaño del conjunto de copias de seguridad, en bytes.<br /><br /> **Nombre de usuario**: <br />                          Nombre del usuario que realizó la operación de copia de seguridad.<br /><br /> **Expiración**: <br />                          Fecha y hora de expiración del conjunto de copias de seguridad.|  
|**Comprobar medio de copia de seguridad**|Llama a una instrucción RESTORE VERIFY_ONLY en los conjuntos de copia de seguridad seleccionados.<br /><br /> Nota: Se trata de una operación de ejecución prolongada y se puede realizar el seguimiento de su progreso y cancelarlo mediante el Monitor de progreso en el Marco de trabajo de cuadro de diálogo.<br /><br /> Este botón permite comprobar la integridad de los archivos de copia de seguridad seleccionados antes de restaurarlos.<br /><br /> Cuando se comprueba la integridad de los conjuntos de copia de seguridad, en el estado de progreso situado en la parte inferior izquierda del cuadro de diálogo se leerá "Comprobando" en lugar de "Ejecutándose".||  
  
## <a name="compatibility-support"></a>Soporte de compatibilidad  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], puede restaurar una base de datos de usuario a partir de una copia de seguridad de la base de datos creada utilizando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior. Sin embargo, las copias de seguridad las bases de datos **maestra**, de **modelos** y **msdb** creadas utilizando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] no pueden restaurarse con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Asimismo, las copias de seguridad creadas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no se pueden restaurar con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utiliza una ruta de acceso predeterminada distinta de la de versiones anteriores. Por tanto, para restaurar una base de datos creada en la ubicación predeterminada de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es preciso usar la opción MOVE.  
  
 Después de restaurar una base de datos de una versión anterior en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la base de datos se actualiza automáticamente. Normalmente, la base de datos está disponible inmediatamente. Pero, si una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tiene índices de texto completo, el proceso de actualización los importa, los restablece o los vuelve a generar, según la configuración de la propiedad del servidor **Opción de actualización de texto completo** . Si la opción de actualización se establece en **Importar** o en **Volver a generar**, los índices de texto completo no estarán disponibles durante la actualización. Dependiendo de la cantidad de datos que se indicen, la operación de importar puede requerir varias horas y la operación de volver a generar puede requerir hasta diez veces más. Tenga en cuenta también que si la opción de actualización se establece en **Importar**y no hay disponible ningún catálogo de texto completo, se vuelven a generar los índices de texto completo asociados.  
  
## <a name="restoring-from-an-encrypted-backup"></a>Restaurar a partir de una copia de seguridad cifrada  
 La restauración requiere que el certificado o la clave asimétrica que se utilizó originalmente para crear la copia de seguridad esté disponible en la instancia en la que se está restaurando. La cuenta de usuario que realiza la restauración debe tener permisos de **VIEW DEFINITIONS** en el certificado o la clave asimétrica. Los certificados utilizados para cifrar la copia de seguridad no deben renovarse ni actualizarse.  
  
## <a name="restoring-from-microsoft-azure-storage"></a>Restaurar desde Almacenamiento de Microsoft Azure  
Seleccione **URL** en la lista desplegable **Tipo de medio de copia de seguridad:** del cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** .  Después, haga clic en **Agregar** para abrir el cuadro de diálogo **Seleccionar una ubicación de archivo de copia de seguridad** , donde puede seleccionar un contenedor de almacenamiento de Azure o de credenciales de SQL Server existente, agregar un nuevo contenedor de almacenamiento de Azure con una firma de acceso compartido o generar una firma de acceso compartido y las credenciales de SQL Server para un contenedor de almacenamiento existente. Una vez conectado a la cuenta de almacenamiento, los archivos de copia de seguridad se muestran en el cuadro de diálogo **Buscar el archivo de copia de seguridad de Microsoft Azure** , donde puede seleccionar el archivo que se va a usar para la restauración.  Vea también [Conectarse a una suscripción de Microsoft Azure](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md).
  
## <a name="see-also"></a>Consulte también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Restaurar una copia de seguridad desde un dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)   
 [Restaurar una base de datos en una transacción marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Restaurar una copia de seguridad del registro de transacciones &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [Ver el contenido de una cinta o un archivo de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)   
 [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copias de seguridad &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [Argumentos RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [Aplicar copias de seguridad de registros de transacción &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
