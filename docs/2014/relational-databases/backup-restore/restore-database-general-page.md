---
title: Restaurar la base de datos (página General) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoredb.general.f1
ms.assetid: 160cf58c-b06a-475f-9a69-2b051e5767ab
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e659023f09701e9e14e852b3ac8c8c2e0642446b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "70154730"
---
# <a name="restore-database-general-page"></a>Restaurar la base de datos (página General)
  Use la página **General** para especificar información sobre las bases de datos de destino y de origen para una operación de restauración de base de datos.  
  
 **Para utilizar SQL Server Management Studio a fin de restaurar una copia de seguridad de base de datos**  
  
-   [Restaurar una copia de seguridad de base de datos &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [Definir un dispositivo lógico de copia de seguridad en una unidad de cinta &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  Cuando especifica una tarea de restauración mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede generar el script [!INCLUDE[tsql](../../includes/tsql-md.md)][RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) correspondiente si hace clic en **Script** y luego selecciona un destino para el script.  
  
## <a name="permissions"></a>Permisos  
 Si la base de datos que se va a restaurar no existe, el usuario debe tener permisos CREATE DATABASE para poder ejecutar RESTORE. Si la base de datos existe, los permisos RESTORE corresponden de forma predeterminada a los miembros de los roles fijos de servidor **sysadmin** y **dbcreator** , y al propietario (**dbo**) de la base de datos.  
  
 Los permisos RESTORE se conceden a los roles en los que la información acerca de la pertenencia está siempre disponible para el servidor. Debido a que la pertenencia a un rol fijo de base de datos solo se puede comprobar cuando la base de datos es accesible y no está dañada, lo que no siempre ocurre cuando se ejecuta RESTORE, los miembros del rol fijo de base de datos **db_owner** no tienen permisos RESTORE.  
  
 La restauración de una copia de seguridad cifrada requiere permisos `VIEW DEFINITION` al certificado o a la clave asimétrica que se usó para el cifrado durante la copia de seguridad.  
  
## <a name="options"></a>Opciones  
  
### <a name="source"></a>Source  
 Las opciones del panel **Restore from**(Restaurar desde) identifican la ubicación de los conjuntos de copia de seguridad para la base de datos y los conjuntos de copia de seguridad que quiere restaurar.  
  
|Término|Definición|  
|----------|----------------|  
|**Base de datos**|Seleccione la base de datos que desea restaurar en la lista desplegable. La lista solo contiene las bases de datos de las que se han realizado copias de seguridad de acuerdo con el historial de copias de seguridad de **msdb** .|  
|**Dispositivo**|Seleccione los dispositivos de copia de seguridad lógicos o físicos (cintas, direcciones URL o archivos) que contienen las copias de seguridad que desee restaurar. Es obligatorio si la copia de seguridad de la base de datos se realizó de otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Para seleccionar uno o varios dispositivos de copia de seguridad lógicos o físicos, haga clic en el botón Examinar, que abre el cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** . En dicho cuadro, puede seleccionar hasta 64 dispositivos pertenecientes a un conjunto de medios. Los dispositivos de cinta deben estar conectados físicamente al equipo donde se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un archivo de copia de seguridad puede estar en un dispositivo de disco local o extraíble. Para obtener más información, vea [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md). También puede seleccionar **Dirección URL** como el tipo de dispositivo de copia de seguridad almacenado en Azure Storage.<br /><br /> Al salir del cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** , el dispositivo seleccionado aparecerá en forma de valores de solo lectura en la lista **Dispositivo** .|  
|**Base de datos**|Seleccione el nombre de la base de datos cuyas copias de seguridad se deben restaurar en el cuadro de lista desplegable.<br /><br /> Nota: Esta lista solo está disponible cuando se selecciona **Dispositivo** . Solo estarán disponibles las bases de datos que tienen copias de seguridad en los dispositivos seleccionados.|  
  
### <a name="destination"></a>Destination  
 Las opciones del panel **Restaurar en** identifican la base de datos y el punto de restauración.  
  
|Término|Definición|  
|----------|----------------|  
|**Base de datos**|Especifique la base de datos de la lista que debe restaurarse. Puede especificar una nueva base de datos o elegir una base de datos existente de la lista desplegable. La lista incluye todas las bases de datos del servidor, y excluye las bases de datos del sistema **master** y **tempdb**.<br /><br /> Nota: Para restaurar una copia de seguridad protegida con contraseña, use la instrucción [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) .|  
|**Restaurar en**|El cuadro **Restaurar en** se establecerá en "A la última copia de seguridad realizada" de forma predeterminada. También puede hacer clic en **Escala de tiempo** para que se muestre el cuadro de diálogo **Escala de tiempo de la copia de seguridad**, que muestra el historial de copias de seguridad de la base de datos en forma de escala de tiempo. Haga clic en **escala de tiempo** para `datetime` designar un específico en el que desea restaurar la base de datos. La base de datos se restaurará al estado en que estaba en este momento especificado. Consulte [Backup Timeline](backup-timeline.md).|  
  
### <a name="restore-plan"></a>Plan de restauraciones  
  
|Término|Definición|  
|----------|----------------|  
|**Conjuntos de copia de seguridad para restaurar**|Muestra los conjuntos de copia de seguridad disponibles para la ubicación especificada. Cada conjunto de copia de seguridad, resultado de una sola operación de copia de seguridad, se distribuye entre todos los dispositivos del conjunto de medios. De forma predeterminada, se sugiere un plan de recuperación para alcanzar el objetivo la operación de restauración según la selección de los conjuntos de copia de seguridad necesarios. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa el historial de copias de seguridad de **msdb** para identificar las copias de seguridad que son necesarias para restaurar una base de datos y crea un plan de restauración. Por ejemplo, para la restauración de una base de datos, el plan de restauración selecciona la copia de seguridad completa más reciente de la base de datos y la siguiente copia de seguridad diferencial más reciente de la base de datos, si ésta existiese. Con el modelo de recuperación completa, el plan de restauración selecciona, a continuación, todas las copias de seguridad de registros siguientes.<br /><br /> Para invalidar el plan de recuperación sugerido, puede cambiar las siguientes selecciones en la cuadrícula. Se anulará automáticamente la selección de aquellas copias de seguridad que dependan de una copia de seguridad cuya selección fue anulada.<br /><br /> **Restaurar**:<br />                          Las casillas activadas indican los conjuntos de copias de seguridad que se restaurarán.<br />**Nombre**: el nombre del conjunto de copia de seguridad.<br />**Componente**: componente del que se ha realizado una copia de seguridad: **base de datos**, **archivo**o ** \<>en blanco** (para registros de transacciones).<br />**Tipo**: el tipo de copia de seguridad realizada: **Completa**, **Diferencial**o **Registro de transacciones**.<br />**Servidor**: nombre de la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que realizó la operación de copia de seguridad.<br />**Base de datos**: el nombre de la base de datos implicada en la operación de copia de seguridad.<br />**Posición**: posición del conjunto de copia de seguridad en el volumen.<br />**Primer LSN**: número de secuencia de registro de la primera transacción del conjunto de copia de seguridad. En blanco para las copias de seguridad de archivos.<br />**Último LSN**: número de secuencia de registro de la última transacción del conjunto de copia de seguridad. En blanco para las copias de seguridad de archivos.<br />**LSN de punto de comprobación**: el número de secuencia de registro (LSN) del punto de control más reciente en el momento en que se creó la copia de seguridad.<br />**LSN completo**: el número de secuencia de registro de la copia de seguridad completa más reciente de la base de datos.<br />**Fecha de inicio**: fecha y hora en que comenzó la operación de copia de seguridad, presentadas en la configuración regional del cliente.<br />**Fecha de finalización**: fecha y hora de finalización de la operación de copia de seguridad, presentadas en la configuración regional del cliente.<br />**Tamaño**: el tamaño del conjunto de copia de seguridad en bytes.<br />**Nombre de usuario**: el nombre del usuario que realizó la operación de copia de seguridad.<br /><br /> **Expiración**: fecha y hora en que expira el conjunto de copia de seguridad.<br /><br /> Las casillas se habilitan solo cuando se activa la casilla **Selección manual** . Esto permite seleccionar los conjuntos de copia de seguridad que deben restaurarse.<br /><br /> Cuando se activa la casilla **Selección manual** , la precisión del plan de restauraciones se comprueba cada vez que se modifica. Si la secuencia de copias de seguridad es incorrecta, aparecerá un mensaje de error.|  
|**Comprobar medio de copia de seguridad**|Llama a una instrucción RESTORE VERIFY_ONLY en los conjuntos de copia de seguridad seleccionados.<br /><br /> Nota: Se trata de una operación de ejecución prolongada y se puede realizar un seguimiento de su progreso y cancelarlo utilizando el Monitor de progreso en el Marco de trabajo de cuadro de diálogo.<br /><br /> Este botón permite comprobar la integridad de los archivos de copia de seguridad seleccionados antes de restaurarlos.<br /><br /> Cuando se comprueba la integridad de los conjuntos de copia de seguridad, en el estado de progreso situado en la parte inferior izquierda del cuadro de diálogo se leerá "Comprobando" en lugar de "Ejecutándose".|  
  
## <a name="compatibility-support"></a>Soporte de compatibilidad  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], puede restaurar una base de datos de usuario a partir de una copia de seguridad de la base de datos creada utilizando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior. Sin embargo, las copias de seguridad las bases de datos **maestra**, de **modelos** y **msdb** creadas utilizando [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] no pueden restaurarse con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Asimismo, las copias de seguridad creadas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no se pueden restaurar con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utiliza una ruta de acceso predeterminada distinta de la de versiones anteriores. Por tanto, para restaurar una base de datos creada en la ubicación predeterminada de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es preciso usar la opción MOVE.  
  
 Después de restaurar una base de datos de una versión anterior en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la base de datos se actualiza automáticamente. Normalmente, la base de datos está disponible inmediatamente. Pero, si una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tiene índices de texto completo, el proceso de actualización los importa, los restablece o los vuelve a generar, según la configuración de la propiedad del servidor **Opción de actualización de texto completo** . Si la opción de actualización se establece en **Importar** o en **Volver a generar**, los índices de texto completo no estarán disponibles durante la actualización. Dependiendo de la cantidad de datos que se indicen, la operación de importar puede requerir varias horas y la operación de volver a generar puede requerir hasta diez veces más. Tenga en cuenta también que cuando la opción de actualización se establece en **importar**, si un catálogo de texto completo no está disponible, se vuelven a generar los índices de texto completo asociados.  
  
## <a name="restoring-from-an-encrypted-backup"></a>Restaurar a partir de una copia de seguridad cifrada  
 La restauración requiere que el certificado o la clave asimétrica que se utilizó originalmente para crear la copia de seguridad esté disponible en la instancia en la que se está restaurando. La cuenta de usuario que realiza la restauración debe tener permisos de `VIEW DEFINITIONS` en el certificado o la clave asimétrica. Los certificados utilizados para cifrar la copia de seguridad no deben renovarse ni actualizarse.  
  
## <a name="restoring-from-azure-storage"></a>Restaurar desde Azure Storage  
 Al restaurar una copia de seguridad almacenada en Azure Storage, la interfaz de usuario de restauración tiene una nueva opción de dispositivo de copia de seguridad. **Dirección URL** en el cuadro de diálogo **Seleccionar dispositivos de copia de seguridad** . Al hacer clic en **Agregar**, esto le llevará al cuadro de diálogo **conectar con Azure** , que le permite especificar la información de la credencial SQL para autenticarse en la cuenta de almacenamiento.  Una vez conectado a la cuenta de almacenamiento, los archivos de copia de seguridad se muestran en el cuadro de diálogo **Buscar un archivo de copia de seguridad en Azure** , donde puede seleccionar el archivo que se va a usar para la restauración.  
  
## <a name="see-also"></a>Consulte también  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [Restaurar una copia de seguridad desde un dispositivo &#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)   
 [Restaurar una base de datos a una transacción marcada &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Restaurar una copia de seguridad del registro de transacciones &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [Ver el contenido de una cinta o un archivo de &#40;de copia de seguridad SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)   
 [Ver las propiedades y el contenido de un dispositivo lógico de copia de seguridad &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)   
 [Conjuntos de medios, familias de medios y conjuntos de copia de seguridad &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [Argumentos de RESTOre &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)   
 [Aplicar copias de seguridad del registro de transacciones &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)  
  
  
