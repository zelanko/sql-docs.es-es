---
title: Inicialización instantánea de archivos de la base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization [SQL Server]
- file initialization [SQL Server]
- IFI [SQL Server]
- database instant file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
author: stevestein
ms.author: sstein
ms.openlocfilehash: 87257431940b527fda01bc1704a519b37b6d4e05
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982446"
---
# <a name="database-file-initialization"></a>Inicialización de archivos de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Los archivos de datos y registro se inicializan para sobrescribir los datos existentes que los archivos eliminados anteriormente hayan dejado en el disco. Los archivos de datos y registro se inicializan por primera vez llenando los archivos con ceros al realizar una de estas operaciones:  
  
- Crear una base de datos.  
- Agregue archivos de registro o datos a una base de datos existente.  
- Aumentar el tamaño de un archivo existente (incluidas las operaciones de crecimiento automático).  
- Restaurar una base de datos o un grupo de archivos.  
  
Inicializar los archivos hace que estas operaciones tarden más. Sin embargo, cuando los datos se escriben en los archivos por primera vez, el sistema operativo no tiene que rellenar los archivos con ceros.  
  
## <a name="instant-file-initialization-ifi"></a>Inicialización instantánea de archivos (IFI)  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los archivos de datos se pueden inicializar de forma instantánea para evitar que se llenen con ceros las operaciones. La inicialización instantánea de archivos le permite ejecutar rápidamente las operaciones con archivos mencionadas anteriormente. La inicialización instantánea de archivos recupera espacio en disco utilizado sin rellenarlo con ceros. En lugar de eso, el contenido del disco se sobrescribe al escribir nuevos datos en los archivos. Los archivos de registro no se pueden inicializar de forma instantánea.  
  
> [!NOTE]
> La inicialización instantánea de archivos solo está disponible en [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] , [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] o en versiones posteriores.  
> 
> [!IMPORTANT]
> La inicialización instantánea de archivos solo está disponible en archivos de datos. Los archivos de registro siempre se llenan con ceros al crearlos o cuando aumenta su tamaño.
  
La inicialización instantánea de archivos solo está disponible si se ha concedido *SE_MANAGE_VOLUME_NAME* a la cuenta de inicio del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los miembros del grupo de administradores de Windows tienen este derecho y pueden concederlo a otros usuarios añadiéndolos a la directiva de seguridad **Realizar tareas de mantenimiento del volumen** .  
  
> [!IMPORTANT]
> Ciertos usos de la característica, como el [Cifrado de datos transparente (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md), pueden evitar la inicialización instantánea de archivos.  
  
Para conceder a una cuenta el permiso `Perform volume maintenance tasks` :  
  
1.  En el equipo en el que se creará el archivo de datos, abra la aplicación **Directiva de seguridad local** (`secpol.msc`).  
  
2.  En el panel izquierdo, expanda **Directivas locales**y, a continuación, haga clic en **Asignación de derechos de usuario**.  
  
3.  En el panel derecho, haga doble clic en **Realizar tareas de mantenimiento del volumen**.  
  
4.  Haga clic en **Agregar usuario o grupo** y agregue la cuenta que ejecuta el servicio SQL Server.  
  
5.  Haga clic en **Aplicar**y, a continuación, cierre todos los cuadros de diálogo de **Directiva de seguridad local** .  

1. Reinicie el servicio SQL Server.

> [!NOTE]
> A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], este permiso se puede conceder a la cuenta de servicio durante la instalación. Si usa la [instalación de línea de comandos](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), agregue el argumento /SQLSVCINSTANTFILEINIT o active la casilla *Conceder el privilegio de realización de tareas de mantenimiento de volumen al servicio del motor de la base de datos de SQL Server* en el [asistente para la instalación](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).

> [!NOTE]
> A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 y versiones posteriores, se puede usar la columna *instant_file_initialization_enabled* de la DMV [sys.dm_server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) para identificar si la inicialización instantánea de archivos está habilitada.

## <a name="remarks"></a>Notas
Si la cuenta de inicio de servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene concedido *SE_MANAGE_VOLUME_NAME*, se registra un mensaje informativo que es similar al siguiente en el registro de errores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el inicio: 

`Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

Si la cuenta de inicio de servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**no** tiene concedido *SE_MANAGE_VOLUME_NAME*, se registra un mensaje informativo que es similar al siguiente en el registro de errores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el inicio: 

`Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y versiones posteriores)

## <a name="security-considerations"></a>Consideraciones de seguridad  
Al usar la inicialización instantánea de archivos (IFI), como el contenido del disco eliminado solo se sobrescribe cuando se escriben nuevos datos en los archivos, una entidad de seguridad no autorizada puede acceder al contenido eliminado hasta que algún otro dato se escriba en una área específica del archivo de datos. Mientras el archivo de la base de datos se adjunte a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], este riesgo de divulgación de la información se reduce mediante la lista de control de acceso discrecional (DACL) del archivo. Esta DACL permite acceder al archivo solo a la cuenta de servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y al administrador local. Sin embargo, cuando el archivo está separado, un usuario o servicio que no tenga *SE_MANAGE_VOLUME_NAME* puede acceder a él. Existe una consideración similar al crear una copia de seguridad de la base de datos: si el archivo de copia de seguridad no está protegido con una DACL adecuada, el contenido eliminado puede estar disponible para un usuario o servicio no autorizado.  

Otra cosa que hay que tener en cuenta es que, cuando un archivo crece usando IFI, un administrador de SQL Server podría acceder a los contenidos de la página sin procesar y ver el contenido que se ha eliminado anteriormente.

Si los archivos de base de datos están hospedados en una red de área de almacenamiento, también es posible que esta presente siempre nuevas páginas inicializadas previamente y puede ser que configurar el sistema operativo para que vuelva a inicializar las páginas cree una sobrecarga innecesaria.
 
> [!NOTE]
> Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instala en un entorno físico seguro, las ventajas de rendimiento que se consiguen al habilitar la inicialización instantánea de archivos pueden superar el riesgo de seguridad que supone, y por eso se recomienda.
  
Si le preocupa la posibilidad de que se divulgue contenido eliminado, realice una de las acciones siguientes o ambas:  
  
- Asegúrese siempre de que los archivos separados y los archivos de copia de seguridad tienen DACL restrictivas.  
- Deshabilite la inicialización instantánea de archivos para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revocando *SE_MANAGE_VOLUME_NAME* de la cuenta de inicio del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

> [!IMPORTANT]
> Si deshabilita la iniciación instantánea de archivos, aumentarán los tiempos de asignación de los archivos de datos.  
  
> [!NOTE]  
> Deshabilitar la inicialización instantánea de archivos solo afecta a los archivos que se han creado o se ha aumentado su tamaño después de que el derecho del usuario se revocara.  
  
## <a name="see-also"></a>Consulte también  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
