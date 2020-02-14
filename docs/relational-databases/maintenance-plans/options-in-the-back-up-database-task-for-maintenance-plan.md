---
title: Tarea Realizar copia de seguridad de la base de datos (Plan de mantenimiento) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.maintplanproperties.logbackup.f1
- sql13.swb.maint.backup.f1
helpviewer_keywords:
- Back Up Database Task dialog box
ms.assetid: ed1ef012-fa14-4ba5-bafe-d1527ba065b3
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 60183a9777098728ee258274a19aca4d65885b87
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68115827"
---
# <a name="options-in-the-back-up-database-task-for-maintenance-plan"></a>Opciones de la tarea Realizar copia de seguridad de la base de datos para el plan de mantenimiento
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice el cuadro de diálogo **Tarea Copia de seguridad de la base de datos** para agregar una tarea de copia de seguridad al plan de mantenimiento. Es importante realizar una copia de seguridad de la base de datos por si se produce un error de sistema o del hardware (o un error del usuario) que cause algún tipo de daño en la base de datos y que requiera una copia de seguridad para la restauración. Esta tarea le permite realizar copias de seguridad completas, diferenciales, de archivos y grupos de archivos, así como de registros de transacciones.  
  
 **Para crear una tarea de copia de seguridad de la base de datos**  
  
-   [Crear un plan de mantenimiento](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
## <a name="options"></a>Opciones  
 **Connection**  
 Seleccione la conexión al servidor que va a utilizar para la realización de esta tarea.  
  
 **Nuevo**  
 Cree una nueva conexión de servidor que utilizará al realizar esta tarea. El cuadro de diálogo **Nueva conexión** se describe a continuación.  
  
 **Bases de datos**  
 Especifique las bases de datos a las que afecta esta tarea. Cuando se selecciona, la lista desplegable proporciona las siguientes opciones: **Todas las bases de datos**, **Todas las bases de datos del sistema**, **Todas las bases de datos de usuario**, **Estas bases de datos**.  
  
 **Todas las bases de datos**  
 Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Todas las bases de datos del sistema (master, msdb y model)**  
 Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No se ejecutarán tareas de mantenimiento en las bases de datos creadas por usuarios.  
  
 **Todas las bases de datos de usuario (master, model y msdb excluidas)**  
 Genera un plan de mantenimiento que ejecuta tareas de mantenimiento en todas las bases de datos creadas por usuarios. No se ejecutarán tareas de mantenimiento en las bases de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Las bases de datos**  
 Genera un plan de mantenimiento que ejecuta tareas de mantenimiento únicamente en las bases de datos seleccionadas. Si elige esta opción, deberá seleccionar al menos una base de datos de la lista.  
  
 **Tipo de copia de seguridad**  
 Muestra el tipo de copia de seguridad que se va a realizar.  
  
 **Componente de copia de seguridad**  
 Seleccione **Base de datos** para realizar una copia de seguridad de toda la base de datos. Seleccione **Archivo y grupos de archivos** para realizar una copia de seguridad únicamente de una parte de la base de datos. Si selecciona esta opción, debe especificar el nombre del archivo o del grupo de archivos. Cuando se seleccionan varias bases de datos en el cuadro **Bases de datos** , solo hay que especificar **Bases de datos** para **Componente de copia de seguridad**. Para realizar copias de seguridad de un archivo o grupo de archivos, cree una tarea para cada base de datos.  
  
 **El conjunto de copia de seguridad expira**  
 Especifica cuándo se puede sobrescribir el conjunto de copia de seguridad con otro conjunto de copia de seguridad.  
  
 **Copia de seguridad en**  
 Realice la copia de seguridad de la base de datos en un archivo o en una cinta. Solo están disponibles los dispositivos de cinta conectados al equipo que contiene la base de datos.  
  
 **Realizar copia de seguridad de las bases de datos en uno o varios archivos**  
 Haga clic en **Agregar** para abrir el cuadro de diálogo **Seleccionar destino de la copia de seguridad** y especificar una o varias ubicaciones del disco o dispositivo de cinta.  
  
 **Si existen copias de seguridad**  
 Seleccione **Anexar** para agregar esta copia de seguridad al final del archivo. Seleccione **Sobrescribir**para quitar todas las copias de seguridad antiguas del archivo y reemplazarlas por esta nueva copia de seguridad.  
  
 **Crear un archivo de copia de seguridad para cada base de datos**  
 Crea un archivo de copia de seguridad en la ubicación especificada en el cuadro de la carpeta. Se creará un archivo para cada base de datos seleccionada.  
  
 **Crear un subdirectorio para cada base de datos**  
 Seleccione esta opción para colocar cada base de datos en una subcarpeta.  
  
> [!IMPORTANT]  
>  Aunque los planes de mantenimiento pueden crear subdirectorios, las tareas de mantenimiento no pueden eliminar subdirectorios. Esta característica reduce la posibilidad de un ataque malintencionado que utilice la tarea Limpieza de mantenimiento para eliminar archivos.  
  
> [!IMPORTANT]  
>  El subdirectorio hereda los permisos del directorio principal. Restrinja los permisos para evitar el acceso no autorizado.  
  
 **Carpeta**  
 Especifica la carpeta que va a contener los archivos de base de datos creados de forma automática.  
  
 **Extensión del archivo de copia de seguridad**  
 Especifique la extensión que se va a utilizar para los archivos de copia de seguridad. El valor predeterminado es **.bak**.  
  
 **Comprobar integridad de copia de seguridad**  
 Comprueba que el conjunto de copias de seguridad está completo y que todos los volúmenes son legibles.  
  
 **Realizar copia de seguridad del final del registro y dejar la base de datos en estado de restauración**  
 Realice una copia de seguridad de registros como último paso antes de restaurar una base de datos. Para obtener más información, vea [Copias del final del registro &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md).  
  
 **Establecer la compresión de copia de seguridad**  
 En [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (o en versiones posteriores), seleccione uno los siguientes valores de [compresión de copia de seguridad](../../relational-databases/backup-restore/backup-compression-sql-server.md) :  
  
|||  
|-|-|  
|**Usar la configuración de servidor predeterminada**|Haga clic para utilizar el valor predeterminado de nivel de servidor.<br /><br /> La opción de la configuración del servidor **Compresión de copia de seguridad predeterminada** establece este valor predeterminado. Para obtener más información sobre cómo ver la configuración actual de esta opción, vea [Ver o establecer la opción de configuración del servidor de compresión de copia de seguridad predeterminada](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).|  
|**Comprimir copia de seguridad**|Haga clic para comprimir la copia de seguridad, sin tener en cuenta el valor predeterminado de nivel de servidor.<br /><br /> **\*\* Importante \*\*** De forma predeterminada, la compresión aumenta significativamente el uso de CPU y la CPU adicional que consume el proceso de compresión puede afectar negativamente a las operaciones simultáneas. Por consiguiente, podría ser conveniente crear copias de seguridad comprimidas de prioridad baja en una sesión en la que el [regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)limite el uso de CPU. Para obtener más información, vea [Usar el regulador de recursos para limitar el uso de CPU mediante compresión de copia de seguridad &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)limite el uso de CPU.|  
|**No comprimir copia de seguridad**|Haga clic para crear una copia de seguridad sin comprimir, independientemente del valor predeterminado de nivel de servidor.|  
  
 **Ver T-SQL**  
 Muestra las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] realizadas en el servidor para esta tarea, en función de las opciones seleccionadas.  
  
> [!NOTE]  
>  Si el número de objetos afectados es elevado, es posible que deba esperar un rato hasta que se muestren.  
  
## <a name="new-connection-dialog-box"></a>Cuadro de diálogo Nueva conexión  
 **Nombre de la conexión**  
 Escriba un nombre para la nueva conexión.  
  
 **Seleccionar o especificar un nombre de servidor**  
 Seleccione un servidor al que conectarse cuando se realice esta tarea.  
  
 **Actualizar**  
 Actualiza la lista de servidores disponibles.  
  
 **Especificar información para iniciar sesión en el servidor**  
 Especifica el modo de autenticación en el servidor.  
  
 **Usar seguridad integrada de Windows NT**  
 Conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] con autenticación de Windows.  
  
 **Utilizar un nombre de usuario y una contraseña específicos**  
 Conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] mediante autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta opción no está disponible.  
  
 **Nombre de usuario**  
 Proporcione un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la autenticación. Esta opción no está disponible.  
  
 **Contraseña**  
 Proporcione una contraseña para que se utilice en la autenticación. Esta opción no está disponible.  
  
## <a name="see-also"></a>Consulte también  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)  
  
  
