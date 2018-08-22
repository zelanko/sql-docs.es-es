---
title: Configuración avanzada para SQL Server Machine Learning Services | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8384773f6db4c0ced2fc68e52cd78100c98c52fd
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40396363"
---
# <a name="advanced-configuration-options-for-sql-server-machine-learning-services"></a>Opciones de configuración avanzada para SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe los cambios que puede realizar después de la instalación, para modificar la configuración de tiempo de ejecución de scripts externos y otros servicios asociados de aprendizaje automático en SQL Server.

**Se aplica a:** SQL Server 2016 R Services, SQL Server 2017 de Machine Learning Services

##  <a name="bkmk_Provisioning"></a> Cuentas de usuario adicional de aprovisionamiento de máquina aprendizaje

Procesa el script externo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecutar en el contexto de las cuentas de usuario local con pocos privilegios. Estos procesos en ejecución en las cuentas individuales con pocos privilegios tiene las siguientes ventajas:

+ Reduce los privilegios de los procesos en tiempo de ejecución de script externo en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo
+ Proporciona aislamiento entre las sesiones de un tiempo de ejecución externo como R o Python.

Como parte de la instalación de un nuevo Windows *grupo de cuentas de usuario* creado que contiene las cuentas de usuario locales necesarias para ejecutar los procesos externos en tiempo de ejecución, como R o Python. Puede modificar el número de usuarios según sea necesario para admitir tareas de aprendizaje automático. 

Además, el Administrador de base de datos debe dar a este grupo permiso para conectarse a cualquier instancia donde se ha habilitado el aprendizaje automático. Para obtener más información, consulte [modificar el grupo de cuentas de usuario de SQL Server Machine Learning Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

A los recursos confidenciales protext en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede definir una lista de control de acceso (ACL) para este grupo. Al especificar que el grupo se deniega el acceso a los recursos, puede impedir el acceso por procesos externos como los tiempos de ejecución de R o Python.

+ El grupo de cuentas de usuario está vinculado a una instancia específica. Se necesita un grupo de cuentas de trabajo independiente para cada instancia de en qué equipo se ha habilitado el aprendizaje. Las cuentas no se pueden compartir entre instancias.

+ Los nombres de las cuentas de usuario del bloque presentan el formato nombreDeInstanciaSQL*nn*. Por ejemplo, si usa la instancia predeterminada para el aprendizaje automático, el grupo de cuentas de usuario admite nombres de cuenta como MSSQLSERVER01, MSSQLSERVER02 y así sucesivamente.

+ El tamaño del grupo de cuentas de usuario es estático y el valor predeterminado es 20. El número de sesiones de tiempo de ejecución externos que se puede iniciar de forma simultánea está limitado por el tamaño de este grupo de cuentas de usuario. Para cambiar este límite, un administrador debe utilizar el Administrador de configuración de SQL Server.

Para obtener más información acerca de cómo realizar cambios en el grupo de cuentas de usuario, consulte [modificar el grupo de cuentas de usuario de SQL Server Machine Learning Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

##  <a name="bkmk_ManagingMemory"></a> Administrar la memoria utilizada por los procesos de script externo

De forma predeterminada, los tiempos de ejecución de scripts externos para el aprendizaje automático se limitan a no más de 20% de memoria total del equipo. Depende de su sistema, pero en general, podría encontrar este límite suficiente para realizar tareas como entrenar un modelo o la predicción del número de filas de datos de aprendizaje automático de graves. 

Para admitir el aprendizaje automático, un administrador puede aumentar este límite. Al hacerlo, deberá reducir la cantidad de memoria reservada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o para otros servicios. También debe considerar el uso del regulador de recursos para definir un grupo de recursos externos o los grupos, por lo que puede asignar grupos de recursos específicos para los trabajos de R o Python.

Para obtener más información, consulte [regulación de recursos de aprendizaje automático](../../advanced-analytics/r/resource-governance-for-r-services.md).


## <a name="bkmk_Launchpad"></a>Modificar la cuenta de servicio Launchpad

Otro [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio se crea para cada instancia en el que ha configurado el servicio machine learning.

De forma predeterminada, Launchpad está configurado para ejecutarse con la cuenta de NT Service\MSSQLLaunchpad, que se aprovisiona con todos los permisos necesarios para ejecutar scripts de R. Sin embargo, si cambia esta cuenta, Launchpad podría no pueda iniciar o tener acceso a la instancia de SQL Server donde se deberían ejecutar scripts externos.

Si se modifica la cuenta de servicio, asegúrese de usar la aplicación **Directiva de seguridad local** y actualice los permisos de las cuentas de servicios para incluir estos permisos:

+ Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)
+ Omitir la comprobación transversal (SeChangeNotifyPrivilege)
+ Iniciar sesión como servicio (SeServiceLogonRight)
+ Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)

Para más información sobre los permisos para ejecutar servicios de SQL Server, vea [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

##  <a name="bkmk_ChangingConfig"></a> Cambiar las opciones avanzadas del servicio

En las primeras versiones de SQL Server 2016 R Services, puede cambiar algunas propiedades del servicio mediante la edición de la [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] archivo de configuración. 

Sin embargo, este archivo ya no se usa para cambiar las configuraciones. Se recomienda que utilice el Administrador de configuración de SQL Server a efecto los cambios realizados en configuración del servicio, como la cuenta de servicio y el número de usuarios.

**Para modificar la configuración de Launchpad**

1. Abra el [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md). 
2. Haga clic en Launchpad de SQL Server y seleccione **propiedades**.

    + Para cambiar la cuenta de servicio, haga clic en el **iniciar sesión** ficha.

    + Para aumentar el número de usuarios, haga clic en el **avanzadas** ficha.


**Para modificar la configuración de depuración**

Algunas propiedades solo pueden cambiarse mediante el uso de archivo de configuración del Launchpad, que puede ser útil en casos limitados, como la depuración. El archivo de configuración se crea durante la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instalación y de forma predeterminada, se guarda como un archivo de texto sin formato en la siguiente ubicación: `<instance path>\binn\rlauncher.config`

Para realizar cambios en este archivo, debe ser administrador en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si edita el archivo, se recomienda realizar una copia de seguridad antes de guardar los cambios.

En la tabla siguiente se enumera las opciones avanzadas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], con los valores permitidos. 

|**Nombre de opción**|**Tipo**|**Descripción**|
|----|----|----|
|TRABAJO\_LIMPIEZA\_ON\_SALIR|Integer |Esto es sólo una opción interna: no cambie este valor. </br></br>Especifica si se debe limpiar la carpeta de trabajo temporal creada para cada sesión externos en tiempo de ejecución una vez completada la sesión. Esta opción resulta útil para la depuración. </br></br>Los valores admitidos son **0** (deshabilitado) o **1** (habilitado). </br></br>El valor predeterminado es 1, se eliminan los archivos de registro de significado al salir.|
|SEGUIMIENTO\_NIVEL|Integer |Configura el nivel de detalle del seguimiento de MSSQLLAUNCHPAD con fines de depuración. Esto afecta a los archivos de seguimiento en la ruta de acceso especificada por la opción LOG_DIRECTORY. </br></br>Los valores admitidos son: **1** (Error), **2** (rendimiento), **3** (advertencia), **4** (información). </br></br>El valor predeterminado es 1, lo que significa que solo advertencias de salida.|

Todas las opciones se presentan como un par clave-valor y cada una de ellas se encuentra en una línea aparte. Por ejemplo, para cambiar el nivel de seguimiento, agregaría la línea `Default: TRACE_LEVEL=4`.

## <a name="see-also"></a>Vea también

[Consideraciones de seguridad](security-considerations-for-the-r-runtime-in-sql-server.md)
