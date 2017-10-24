---
title: "Configuración las opciones avanzadas para servicios de aprendizaje de máquina | Documentos de Microsoft"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 872acf107d72989b4623a9d5f4ccb85c44d1f2f9
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="advanced-configuration-options-for-machine-learning-services"></a>Configuración las opciones avanzadas para servicios de aprendizaje automático

Este artículo describe los cambios que pueden realizar después de la instalación, para modificar la configuración de tiempo de ejecución de R y otros servicios asociados con el aprendizaje automático en SQL Server.

Se aplica a: servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

##  <a name="bkmk_Provisioning"></a>Aprovisionar las cuentas de usuario para la máquina aprendizaje

Script externo de los procesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecutan en el contexto de las cuentas de usuario local con pocos privilegios. Estos procesos en ejecución en cuentas con pocos privilegios individuales tiene las siguientes ventajas:

+ Reduce los privilegios de los procesos en tiempo de ejecución de script externo en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo
+ Proporciona aislamiento entre las sesiones de un tiempo de ejecución externo, como R o Python.

Como parte del programa de instalación, una nueva ventana de *grupo de cuentas de usuario* creado que contiene las cuentas de usuario local necesarias para ejecutar el proceso de tiempo de ejecución de R. Puede modificar el número de usuarios si es necesario para admitir R. El administrador de base de datos también debe asignar a este grupo permiso para conectarse a cualquier instancia donde se haya habilitado R Services. Para obtener más información, consulte [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

Pero se puede definir una lista de control de acceso (ACL) para recursos confidenciales en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para denegar el acceso a este grupo con el fin de evitar que el proceso del tiempo de ejecución de R pueda obtener acceso a los recursos.

+ El grupo de cuentas de usuario está vinculado a una instancia específica.  Para cada instancia en la que se haya habilitado el script de R, se crea un grupo de trabajo independiente de cuentas de trabajador. Las cuentas no se pueden compartir entre instancias.

+ Los nombres de las cuentas de usuario del bloque presentan el formato nombreDeInstanciaSQL*nn*. Por ejemplo, si usa la instancia predeterminada como el servidor de R, el grupo de cuentas de usuario presentará nombres de cuenta como MSSQLSERVER01, MSSQLSERVER02 y así sucesivamente.

+ El tamaño del grupo de cuentas de usuario es estático y el valor predeterminado es 20. El número de sesiones del runtime de R que se puede iniciar de forma simultánea está limitado por el tamaño de este grupo de cuentas de usuario. Pero un administrador puede cambiar este límite mediante el Administrador de configuración de SQL Server.

Para obtener más información sobre cómo realizar cambios en el grupo de cuentas de usuario, consulte [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

##  <a name="bkmk_ManagingMemory"></a>Administrar la memoria utilizada por los procesos de Script externo

De forma predeterminada, los procesos del runtime de R asociados con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] no pueden utilizar más de un 20 % de la memoria total de la máquina. Sin embargo, el administrador puede incrementar este límite, si resulta necesario.

Por lo general, esta cantidad será suficiente para tareas de R graves como el modelo de entrenamiento o la predicción del número de filas de datos. Es posible que tenga que reducir la cantidad de memoria reservada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o para otros servicios) y usar el regulador de recursos para definir y asignar un grupo (o grupos) de recursos externos. Para obtener más información, consulte [regulador de recursos para R](../../advanced-analytics/r/resource-governance-for-r-services.md).

##  <a name="bkmk_ChangingConfig"></a>Cambiar las opciones de servicio avanzado mediante el archivo de configuración

Se pueden controlar algunas propiedades avanzadas de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] modificando el archivo de configuración de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. Este archivo se crea durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, de manera predeterminada, se guarda como un archivo de texto sin formato en la siguiente ubicación:

`<instance path>\binn\rlauncher.config`

Para realizar cambios en este archivo, debe ser administrador en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si edita el archivo, se recomienda realizar una copia de seguridad antes de guardar los cambios.

Por ejemplo, para usar el Bloc de notas para abrir el archivo de configuración para la instancia predeterminada, podría abrir un símbolo del sistema como administrador y escriba el siguiente comando:

```
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
```

##  <a name="bkmk_properties"></a>Editar propiedades de configuración

En la siguiente tabla se muestra cada una de las configuraciones admitidas para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], con los valores permitidos.

Todas las opciones se presentan como un par clave-valor y cada una de ellas se encuentra en una línea aparte. Por ejemplo, esta propiedad especifica el nivel de seguimiento para RLauncher:

Valor predeterminado: TRACE_LEVEL=4


|**Nombre de opción**|**Tipo de valor**|**Valor de DB-Library**|**Descripción**|
|------------------|----------------|-------------|-----------------|
|JOB_CLEANUP_ON_EXIT|Integer<br /><br /> 0 = Deshabilitado<br /><br /> 1 = Habilitado|1<br /><br /> Los archivos de registro se eliminan al salir.|Especifica si se debe limpiar la carpeta de trabajo temporal creada para cada sesión de R una vez completada esta última. Esta opción resulta útil para la depuración.<br /><br /> Nota: Se trata únicamente de una opción interna: no cambie este valor.|
|TRACE_LEVEL|Integer<br /><br /> 1 = error<br /><br /> 2 = rendimiento<br /><br /> 3 = advertencia<br /><br /> 4 = información|1<br /><br /> Solo advertencias de salida|Configura el nivel de detalle del seguimiento del iniciador de R (MSSQLLAUNCHPAD) con fines de depuración. Esta opción afecta al nivel de detalle de los seguimientos almacenados en los siguientes archivos de seguimiento, ambos ubicados en la ruta de acceso especificada por la opción LOG_DIRECTORY:<br /><br /> **rlauncher.log**: archivo de seguimiento generado para las sesiones de R iniciadas por consultas de T-SQL.<br /><br /> |

## <a name="bkmk_Launchpad"></a>Modificar la cuenta de servicio de Launchpad

Otro [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio se crea para cada instancia en la que ha configurado los servicios de aprendizaje automático.

De forma predeterminada, Launchpad está configurado para ejecutarse con la cuenta de NT Service\MSSQLLaunchpad, que se aprovisiona con todos los permisos necesarios para ejecutar scripts de R. Sin embargo, si cambia esta cuenta, Launchpad posible que no pueda iniciarse o tener acceso a la instancia de SQL Server donde se deberían ejecutar scripts externos.

Si se modifica la cuenta de servicio, asegúrese de usar la aplicación **Directiva de seguridad local** y actualice los permisos de las cuentas de servicios para incluir estos permisos:

+ Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)
+ Omitir la comprobación transversal (SeChangeNotifyPrivilege)
+ Iniciar sesión como servicio (SeServiceLogonRight)
+ Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)

Para más información sobre los permisos para ejecutar servicios de SQL Server, vea [Configurar los permisos y las cuentas de servicio de Windows](https://msdn.microsoft.com/library/ms143504.aspx#Windows).

## <a name="see-also"></a>Vea también

[Consideraciones de seguridad](security-considerations-for-the-r-runtime-in-sql-server.md)

