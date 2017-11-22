---
title: "Configuración las opciones avanzadas para servicios de aprendizaje de máquina | Documentos de Microsoft"
ms.custom: SQL2016_New_Updated
ms.date: 10/31/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 369c630e249d7775e67508fc9b00e94447182012
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="advanced-configuration-options-for-machine-learning-services"></a>Opciones de configuración avanzada de servicios de aprendizaje de máquina

Este artículo describe los cambios que pueden realizar después de la instalación, para modificar la configuración de tiempo de ejecución de scripts externos y otros servicios asociados con el aprendizaje automático en SQL Server.

**Se aplica a:** servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

##  <a name="bkmk_Provisioning"></a>Cuentas de usuario adicional de aprovisionamiento para la máquina aprendizaje

Script externo de los procesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecutan en el contexto de las cuentas de usuario local con pocos privilegios. Estos procesos en ejecución en cuentas con pocos privilegios individuales tiene las siguientes ventajas:

+ Reduce los privilegios de los procesos en tiempo de ejecución de script externo en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equipo
+ Proporciona aislamiento entre las sesiones de un tiempo de ejecución externo, como R o Python.

Como parte del programa de instalación, una nueva ventana de *grupo de cuentas de usuario* creado que contiene las cuentas de usuario local necesarias para ejecutar procesos externos en tiempo de ejecución, como R o Python. Puede modificar el número de usuarios según sea necesario para admitir tareas de aprendizaje automático. 

Además, el Administrador de base de datos debe asignar a este grupo permiso para conectarse a cualquier instancia donde se ha habilitado el aprendizaje automático. Para obtener más información, consulte [modificar el grupo de cuentas de usuario para servicios de aprendizaje de máquina de SQL Server](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

A los recursos confidenciales protext en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede definir una lista de control de acceso (ACL) para este grupo. Mediante la especificación de recursos que el grupo se deniega el acceso, puede impedir el acceso por parte de procesos externos, como los tiempos de ejecución de R o Python.

+ El grupo de cuentas de usuario está vinculado a una instancia específica. Se necesita un grupo de cuentas de trabajo independiente para cada instancia de en qué equipo se ha habilitado el aprendizaje. Las cuentas no se pueden compartir entre instancias.

+ Los nombres de las cuentas de usuario del bloque presentan el formato nombreDeInstanciaSQL*nn*. Por ejemplo, si está utilizando la instancia predeterminada para el aprendizaje automático, el grupo de cuentas de usuario admite nombres de cuenta como MSSQLSERVER01, MSSQLSERVER02 y así sucesivamente.

+ El tamaño del grupo de cuentas de usuario es estático y el valor predeterminado es 20. El número de sesiones de externo en tiempo de ejecución que puede iniciar de forma simultánea está limitado por el tamaño de este grupo de cuentas de usuario. Para cambiar este límite, un administrador debe utilizar el Administrador de configuración de SQL Server.

Para obtener más información acerca de cómo realizar cambios en el grupo de cuentas de usuario, consulte [modificar el grupo de cuentas de usuario para servicios de aprendizaje de máquina de SQL Server](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

##  <a name="bkmk_ManagingMemory"></a>Administrar la memoria utilizada por los procesos de script externo

De forma predeterminada, los tiempos de ejecución de script externo para el aprendizaje automático se limitan a no más del 20% de memoria total de la máquina. Depende de su sistema, pero en general, podría encontrar este límite es insuficiente para tareas de aprendizaje de máquina graves como entrenar un modelo o de predicción en varias filas de datos. 

Para admitir el aprendizaje automático, un administrador puede aumentar este límite. Al hacerlo, tendrá que reducir la cantidad de memoria reservada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o para otros servicios. También debe considerar la utilización de regulador de recursos para definir un grupo de recursos externos o grupos, por lo que puede asignar grupos de recursos específicos para los trabajos de R o Python.

Para obtener más información, consulte [regulador de recursos para el aprendizaje automático](../../advanced-analytics/r/resource-governance-for-r-services.md).


## <a name="bkmk_Launchpad"></a>Modificar la cuenta de servicio de Launchpad

Otro [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio se crea para cada instancia en la que ha configurado los servicios de aprendizaje automático.

De forma predeterminada, Launchpad está configurado para ejecutarse con la cuenta de NT Service\MSSQLLaunchpad, que se aprovisiona con todos los permisos necesarios para ejecutar scripts de R. Sin embargo, si cambia esta cuenta, Launchpad posible que no pueda iniciarse o tener acceso a la instancia de SQL Server donde se deberían ejecutar scripts externos.

Si se modifica la cuenta de servicio, asegúrese de usar la aplicación **Directiva de seguridad local** y actualice los permisos de las cuentas de servicios para incluir estos permisos:

+ Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)
+ Omitir la comprobación transversal (SeChangeNotifyPrivilege)
+ Iniciar sesión como servicio (SeServiceLogonRight)
+ Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)

Para más información sobre los permisos para ejecutar servicios de SQL Server, vea [Configurar los permisos y las cuentas de servicio de Windows](https://msdn.microsoft.com/library/ms143504.aspx#Windows).

##  <a name="bkmk_ChangingConfig"></a>Cambiar las opciones avanzadas del servicio

En las versiones anteriores de SQL Server 2016 R Services, puede cambiar algunas propiedades del servicio mediante la edición de la [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] archivo de configuración. 

Sin embargo, este archivo ya no se utiliza para cambiar las configuraciones. Recomendamos que utilice el Administrador de configuración de SQL Server a los cambios de efecto a la configuración de servicio, como la cuenta de servicio y el número de usuarios.

**Para modificar la configuración de Launchpad**

1. Abra el [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md). 
2. Haga clic en Launchpad de SQL Server y seleccione **propiedades**.

    + Para cambiar la cuenta de servicio, haga clic en el **Log On** ficha.

    + Para aumentar el número de usuarios, haga clic en el **avanzadas** ficha.


**Para modificar la configuración de depuración**

Algunas propiedades solo pueden cambiarse mediante el uso de archivo de configuración del Launchpad, que podría ser útil en casos limitados, como la depuración. El archivo de configuración se crea durante la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación y de forma predeterminada, se guarda como un archivo de texto sin formato en la siguiente ubicación:`<instance path>\binn\rlauncher.config`

Para realizar cambios en este archivo, debe ser administrador en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si edita el archivo, se recomienda realizar una copia de seguridad antes de guardar los cambios.

La tabla siguiente muestra la configuración avanzada de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], con los valores permitidos. 

|**Nombre de opción**|**Tipo**|**Description**|
|----|----|----|
|TRABAJO\_LIMPIEZA\_ON\_SALIR|Integer |Se trata únicamente una opción interna: no cambie este valor. </br></br>Especifica si se debe limpiar la carpeta de trabajo temporal creada para cada sesión externo en tiempo de ejecución una vez completada la sesión. Esta opción resulta útil para la depuración. </br></br>Los valores admitidos son **0** (deshabilitado) o **1** (habilitado). </br></br>El valor predeterminado es 1, los archivos de registro de significado se eliminan al salir.|
|SEGUIMIENTO\_NIVEL|Integer |Configura el nivel de detalle del seguimiento de MSSQLLAUNCHPAD para fines de depuración. Esto afecta a los archivos de seguimiento en la ruta de acceso especificada por la opción LOG_DIRECTORY. </br></br>Los valores admitidos son: **1** (Error), **2** (rendimiento), **3** (advertencia), **4** (información). </br></br>El valor predeterminado es 1, lo que significa que solo advertencias de salida.|

Todas las opciones se presentan como un par clave-valor y cada una de ellas se encuentra en una línea aparte. Por ejemplo, para cambiar el nivel de seguimiento, se agregará la línea `Default: TRACE_LEVEL=4`.

## <a name="see-also"></a>Vea también

[Consideraciones de seguridad](security-considerations-for-the-r-runtime-in-sql-server.md)
