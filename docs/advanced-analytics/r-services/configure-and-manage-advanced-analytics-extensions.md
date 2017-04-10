---
title: "Configuraci&#243;n y administraci&#243;n de Extensiones de an&#225;lisis avanzados | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 20
---
# Configuraci&#243;n y administraci&#243;n de Extensiones de an&#225;lisis avanzados
  Una vez que se haya instalado [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], podrá realizar cambios menores en la configuración del runtime de R y otros servicios asociados a [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] .  
  
  
 **En este tema**  
  
-   [Aprovisionamiento de cuentas de usuario para SQL Server R Services](#bkmk_Provisioning)  
  
-   [Administración del uso de memoria permitido a los procesos de R](#bkmk_ManagingMemory)  
  
-   [Cambio de los valores predeterminados del servicio mediante el archivo de configuración](#bkmk_ChangingConfig) 

-   [Modificación de la cuenta de servicio Launchpad](#bkmk_Launchpad) 
  
##  <a name="bkmk_Provisioning"></a> Aprovisionamiento de cuentas de usuario para SQL Server R Services  
 R en tiempo de ejecución de los procesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecutan en el contexto de cuentas de usuario local con pocos privilegios. La ejecución de procesos del runtime de R en cuentas individuales con pocos privilegios reporta las siguientes ventajas:  
  
-   Reducir los privilegios de los procesos del runtime de R en el equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
  
-   Proporcionar aislamiento entre las sesiones del runtime de R  
  
 Como parte del proceso de instalación en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], una nueva ventana de *grupo de cuenta de usuario* creado que contiene las cuentas de usuario locales necesarias para ejecutar el proceso de tiempo de ejecución de R. Puede modificar el número de usuarios si es necesario para admitir R. El Administrador de la base de datos también debe asignar a este grupo permiso para conectarse a cualquier instancia donde se ha habilitado Servicios de R. Para obtener más información, consulte [modificar el grupo de la cuenta de usuario de servicios de SQL Server R](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).  
  
 Sin embargo, se puede definir una lista de control de acceso (ACL) para recursos confidenciales en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para denegar el acceso a este grupo para impedir que el proceso de tiempo de ejecución de R al obtener acceso a los recursos.  
  
-   El grupo de la cuenta de usuario está vinculado a una instancia específica.  Para cada instancia en qué R se ha habilitado la secuencia de comandos, un grupo de trabajo independiente, se crean las cuentas. Las cuentas no se pueden compartir entre instancias.
  
-   Los nombres de las cuentas de usuario del bloque presentan el formato nombreDeInstanciaSQL*nn*. Por ejemplo, si usa la instancia predeterminada como el servidor de R, el grupo de cuentas de usuario presentará nombres de cuenta como MSSQLSERVER01, MSSQLSERVER02 y así sucesivamente.  
  
-   El tamaño del grupo de cuentas de usuario es estático y el valor predeterminado es 20. El número de sesiones del runtime de R que se puede iniciar de forma simultánea está limitado por el tamaño de este grupo de cuentas de usuario. Sin embargo, este límite puede cambiarse por un administrador mediante el uso de SQL Server Configuration Manager.  
  
  
 Para obtener más información sobre cómo realizar cambios en el grupo de cuentas de usuario, consulte [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).  
  
##  <a name="bkmk_ManagingMemory"></a> Administración del uso de memoria permitido a los procesos de R  
 De forma predeterminada, los procesos del runtime de R asociados con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] no pueden utilizar más de un 20 % de la memoria total de la máquina. Sin embargo, el administrador puede incrementar este límite, si resulta necesario.  
  
 Por lo general, esta cantidad será suficiente para tareas de R graves como modelo de entrenamiento o predecir el número de filas de datos. Tendrá que reducir la cantidad de memoria reservada para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o para otros servicios) y utilizar el regulador de recursos para definir un grupo de recursos externos o grupos y asignar. Para obtener más información, consulte [regulador de recursos para los servicios R](../../advanced-analytics/r-services/resource-governance-for-r-services.md).  
  
##  <a name="bkmk_ChangingConfig"></a> Cambiar opciones avanzadas de servicio mediante el archivo de configuración  
 
Puede controlar algunas de las propiedades avanzadas [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] editando la [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] archivo de configuración. Este archivo se crea durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, de manera predeterminada, se guarda como un archivo de texto sin formato en la siguiente ubicación:  
 
```  
<instance path>\binn\rlauncher.config  
```  
  
 Para realizar cambios en este archivo, debe ser administrador en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si edita el archivo, se recomienda realizar una copia de seguridad antes de guardar los cambios.  
  
 Por ejemplo, si desea usar el Bloc de notas para abrir el archivo de configuración de la instancia predeterminada (MSSQLSERVER), tendrá que abrir un símbolo del sistema como administrador y escribir el siguiente comando:  
  
```  
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
  
```  
  
###  <a name="bkmk_properties"></a> Propiedades de configuración  
 Todas las opciones se presentan como un par clave-valor y cada una de ellas se encuentra en una línea aparte. Por ejemplo, esta propiedad especifica que los procesos de R no pueden utilizar más del 20 % de memoria:  
  
 Predeterminado: `MEMORY_LIMIT_PERCENT=20`  
  
 La siguiente tabla muestra cada una de las configuraciones admitidas por [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], con los valores permitidos.  
  
|Nombre de opción|Tipo de valor|Valor de DB-Library|Descripción|  
|------------------|----------------|-------------|-----------------|  
|JOB_CLEANUP_ON_EXIT|Integer<br /><br /> 0 = Deshabilitado<br /><br /> 1 = Habilitado|1<br /><br /> Los archivos de registro se eliminan al salir.|Especifica si se debe limpiar la carpeta de trabajo temporal creada para cada sesión de R una vez completada esta última. Esta opción resulta útil para la depuración.<br /><br /> Nota: Se trata únicamente de una opción interna: no cambie este valor.|  
|TRACE_LEVEL|Integer<br /><br /> 1 = error<br /><br /> 2 = rendimiento<br /><br /> 3 = advertencia<br /><br /> 4 = información|1<br /><br /> Solo advertencias de salida|Configura el nivel de detalle del seguimiento del iniciador de R (MSSQLLAUNCHPAD) con fines de depuración. Esta opción afecta al nivel de detalle de los seguimientos almacenados en los siguientes archivos de seguimiento, ambos ubicados en la ruta de acceso especificada por la opción LOG_DIRECTORY:<br /><br /> **rlauncher.log**: el archivo de seguimiento generado para las sesiones de R iniciadas por consultas de T-SQL.<br /><br /> Para más información sobre este escenario, consulte [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).|  

## <a name="bkmk_Launchpad"></a>Modificación de la cuenta de servicio Launchpad

Otro [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio se crea para cada instancia en la que ha configurado [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]. 

De forma predeterminada, Launchpad está configurado para ejecutarse con la cuenta de NT Service\MSSQLLaunchpad, que se haya aprovisionado con todos los permisos necesarios para ejecutar scripts de R. Sin embargo, si cambia esta cuenta, Launchpad no puede iniciar o tener acceso a la instancia de SQL Server donde se deben ejecutar los scripts de R.
 
  Si modifica la cuenta de servicio, asegúrese de utilizar el **Directiva de seguridad Local** aplicación y actualizar los permisos de cada servicio de cuenta para incluir estos permisos:
  + Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)
  + Omitir la comprobación transversal (SeChangeNotifyPrivilege)
  + Iniciar sesión como servicio (SeServiceLogonRight)
  + Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)

Para obtener más información acerca de los permisos necesarios para ejecutar los servicios de SQL Server, vea [Configurar cuentas de servicio de Windows y permisos](https://msdn.microsoft.com/library/ms143504.aspx#Windows).
   
## Vea también  
 [Introducción a SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  