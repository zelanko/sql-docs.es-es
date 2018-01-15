---
title: "Inicialización instantánea de archivos de la base de datos | Microsoft Docs"
ms.custom: 
ms.date: 01/09/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization [SQL Server]
- file initialization [SQL Server]
- IFI [SQL Server]
- database instant file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: cf0f0006186bde39228ac9b0039e5a45b42431b7
ms.sourcegitcommit: b4b7cd787079fa3244e77c1e9e3c68723ad30ad4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/10/2018
---
# <a name="database-file-initialization"></a>Inicialización de archivos de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Los archivos de datos y registro se inicializan para sobrescribir los datos existentes que los archivos eliminados anteriormente hayan dejado en el disco. Los archivos de datos y registro se inicializan por primera vez llenando los archivos con ceros al realizar una de estas operaciones:  
  
- Crear una base de datos.  
- Agregue archivos de registro o datos a una base de datos existente.  
- Aumentar el tamaño de un archivo existente (incluidas las operaciones de crecimiento automático).  
- Restaurar una base de datos o un grupo de archivos.  
  
Inicializar los archivos hace que estas operaciones tarden más. Sin embargo, cuando los datos se escriben en los archivos por primera vez, el sistema operativo no tiene que rellenar los archivos con ceros.  
  
## <a name="instant-file-initialization-ifi"></a>Inicialización instantánea de archivos (IFI)  
En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los archivos de datos se pueden inicializar de forma instantánea para evitar que se llenen con ceros las operaciones. La inicialización instantánea de archivos le permite ejecutar rápidamente las operaciones con archivos mencionadas anteriormente. La inicialización instantánea de archivos recupera espacio en disco utilizado sin rellenarlo con ceros. En lugar de eso, el contenido del disco se sobrescribe al escribir nuevos datos en los archivos. Los archivos de registro no se pueden inicializar de forma instantánea.  
  
> [!NOTE]  
> La inicialización instantánea de archivos solo está disponible en [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[winxppro](../../includes/winxppro-md.md)] , [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] o en versiones posteriores.  

> [!IMPORTANT]
> La inicialización instantánea de archivos solo está disponible en archivos de datos. Los archivos de registro siempre se llenan con ceros al crearlos o cuando aumenta su tamaño.
  
La inicialización instantánea de archivos solo está disponible si se ha concedido *SE_MANAGE_VOLUME_NAME* a la cuenta de inicio del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los miembros del grupo de administradores de Windows tienen este derecho y pueden concederlo a otros usuarios añadiéndolos a la directiva de seguridad **Realizar tareas de mantenimiento del volumen** .  
  
> [!IMPORTANT]
> Ciertos usos de la característica, como el [Cifrado de datos transparente (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md), pueden evitar la inicialización instantánea de archivos.  
  
Para conceder a una cuenta el permiso `Perform volume maintenance tasks` :  
  
1.  En el equipo en el que se creará el archivo de copia de seguridad, abra la aplicación **Directiva de seguridad local** (`secpol.msc`).  
  
2.  En el panel izquierdo, expanda **Directivas locales**y, a continuación, haga clic en **Asignación de derechos de usuario**.  
  
3.  En el panel derecho, haga doble clic en **Realizar tareas de mantenimiento del volumen**.  
  
4.  Haga clic en **Agregar usuario o grupo** y añada las cuentas de usuario que se utilicen para las copias de seguridad.  
  
5.  Haga clic en **Aplicar**y, a continuación, cierre todos los cuadros de diálogo de **Directiva de seguridad local** .  

> [!NOTE]
> A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], este permiso se puede conceder a la cuenta de servicio durante la instalación. Si usa la [instalación de línea de comandos](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), agregue el argumento /SQLSVCINSTANTFILEINIT o active la casilla *Conceder el privilegio de realización de tareas de mantenimiento de volumen al servicio del motor de la base de datos de SQL Server* en el [asistente para la instalación](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).

> [!NOTE]
> A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 y desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], se puede usar la columna *instant_file_initialization_enabled* en el DMV [sys.dm_server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) para identificar si la inicialización instantánea de archivos está habilitada.

## <a name="remarks"></a>Notas
Si la cuenta de inicio de servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene concedido *SE_MANAGE_VOLUME_NAME*, se registra un mensaje informativo que es similar al siguiente en el registro de errores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el inicio: 

```
Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

Si la cuenta de inicio de servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **no** tiene concedido *SE_MANAGE_VOLUME_NAME*, se registra un mensaje informativo que es similar al siguiente en el registro de errores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el inicio: 

```
Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4, [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 y desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)])

## <a name="security-considerations"></a>Consideraciones de seguridad  
Al usar la inicialización instantánea de archivos (IFI), como el contenido del disco eliminado solo se sobrescribe cuando se escriben nuevos datos en los archivos, una entidad de seguridad no autorizada puede acceder al contenido eliminado hasta que algún otro dato se escriba en una área específica del archivo de datos. Mientras el archivo de la base de datos se adjunte a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], este riesgo de divulgación de la información se reduce mediante la lista de control de acceso discrecional (DACL) del archivo. Esta DACL permite acceder al archivo solo a la cuenta de servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y al administrador local. Sin embargo, cuando el archivo está separado, un usuario o servicio que no tenga *SE_MANAGE_VOLUME_NAME* puede acceder a él. Existe una consideración similar al crear una copia de seguridad de la base de datos: si el archivo de copia de seguridad no está protegido con una DACL adecuada, el contenido eliminado puede estar disponible para un usuario o servicio no autorizado.  
 
> [!NOTE]
> Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instala en un entorno físico seguro, las ventajas de rendimiento que se consiguen al habilitar la inicialización instantánea de archivos pueden superar el riesgo de seguridad que supone, y por eso se recomienda.
  
Si le preocupa la posibilidad de que se divulgue contenido eliminado, realice una de las acciones siguientes o ambas:  
  
- Asegúrese siempre de que los archivos separados y los archivos de copia de seguridad tienen DACL restrictivas.  
- Deshabilite la inicialización instantánea de archivos para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revocando *SE_MANAGE_VOLUME_NAME* de la cuenta de inicio del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

> [!IMPORTANT]
> Si deshabilita la iniciación instantánea de archivos, aumentarán los tiempos de asignación de los archivos de datos.  
  
> [!NOTE]  
> Deshabilitar la inicialización instantánea de archivos solo afecta a los archivos que se han creado o se ha aumentado su tamaño después de que el derecho del usuario se revocara.  
  
## <a name="see-also"></a>Ver también  
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
