---
title: Configuración de cuenta de servicio de SQL Server Launchpad | Microsoft Docs
description: Cómo modificar la cuenta de servicio de SQL Server Launchpad usa para la ejecución de scripts externos en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 76087367c1ba24894989038fb6fc22427d8be77b
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "46712728"
---
# <a name="sql-server-launchpad-service-configuration"></a>Configuración del servicio Launchpad de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Otro [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio se crea para cada instancia del motor de base de datos a la que se ha agregado la integración de SQL Server machine learning (R o Python).

## <a name="account-permissions"></a>Permisos de cuenta

De forma predeterminada, Launchpad de SQL Server está configurado para ejecutarse bajo **NT Service\MSSQLLaunchpad**, que se aprovisiona con todos los permisos necesarios para ejecutar scripts externos. Eliminación de los permisos de esta cuenta puede dar lugar a Launchpad no se pudo iniciar o para tener acceso a la instancia de SQL Server donde se deberían ejecutar scripts externos.

Si modifica la cuenta de servicio, asegúrese de usar el **directiva de seguridad Local** aplicación (**todas las aplicaciones** > **herramientas administrativas de Windows**  >  **Directiva de seguridad local**).

Los permisos necesarios para esta cuenta se muestran en la tabla siguiente.

| Configuración de directiva de grupo | Nombre de constante |
|----------------------|---------------|
| [Ajustar las cuotas de memoria para un proceso](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [Omitir comprobación de recorrido](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [Inicie sesión como un servicio](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [Reemplazar un token de nivel de proceso](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

Para más información sobre los permisos para ejecutar servicios de SQL Server, vea [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>Propiedades de configuración

Normalmente, no hay ninguna razón para modificar la configuración del servicio. Las propiedades que podrían cambiarse incluyen la cuenta de servicio, el número de procesos externos (20 de forma predeterminada) o la contraseña de la directiva para cuentas de trabajo de restablecimiento.

1. Abra el [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md). 

  + En la página de inicio, escriba **MMC** para abrir Microsoft Management Console.
  + En **archivo** > **agregar o quitar complemento**, mover **Administrador de configuración de SQL Server** de disponible para los complementos seleccionados.

2. En SQL Server Configuration Manager en servicios de SQL Server, haga clic en Launchpad de SQL Server y seleccione **propiedades**.

    + Para cambiar la cuenta de servicio, haga clic en el **iniciar sesión** ficha.

    + Para aumentar el número de usuarios, haga clic en el **avanzadas** ficha.

> [!Note]
> En las primeras versiones de SQL Server 2016 R Services, puede cambiar algunas propiedades del servicio mediante la edición de la [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] archivo de configuración. Este archivo ya no se usa para cambiar las configuraciones. Administrador de configuración de SQL Server es el enfoque correcto para los cambios de configuración del servicio, como la cuenta de servicio y el número de usuarios.

## <a name="debug-settings"></a>Configuración de depuración

Algunas propiedades solo pueden cambiarse mediante el uso de archivo de configuración del Launchpad, que puede ser útil en casos limitados, como la depuración. El archivo de configuración se crea durante la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instalación y de forma predeterminada, se guarda como un archivo de texto sin formato en la siguiente ubicación: `<instance path>\binn\rlauncher.config`

Para realizar cambios en este archivo, debe ser administrador en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si edita el archivo, se recomienda realizar una copia de seguridad antes de guardar los cambios.

En la tabla siguiente se enumera las opciones avanzadas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], con los valores permitidos. 

|**Nombre de opción**|**Tipo**|**Descripción**|
|----|----|----|
|TRABAJO\_LIMPIEZA\_ON\_SALIR|Integer |Esto es sólo una opción interna: no cambie este valor. </br></br>Especifica si se debe limpiar la carpeta de trabajo temporal creada para cada sesión externos en tiempo de ejecución una vez completada la sesión. Esta opción resulta útil para la depuración. </br></br>Los valores admitidos son **0** (deshabilitado) o **1** (habilitado). </br></br>El valor predeterminado es 1, se eliminan los archivos de registro de significado al salir.|
|SEGUIMIENTO\_NIVEL|Integer |Configura el nivel de detalle del seguimiento de MSSQLLAUNCHPAD con fines de depuración. Esto afecta a los archivos de seguimiento en la ruta de acceso especificada por la opción LOG_DIRECTORY. </br></br>Los valores admitidos son: **1** (Error), **2** (rendimiento), **3** (advertencia), **4** (información). </br></br>El valor predeterminado es 1, lo que significa que solo advertencias de salida.|

Todas las opciones se presentan como un par clave-valor y cada una de ellas se encuentra en una línea aparte. Por ejemplo, para cambiar el nivel de seguimiento, agregaría la línea `Default: TRACE_LEVEL=4`.

## <a name="see-also"></a>Vea también

[Marco de extensibilidad](../concepts/extensibility-framework.md)
