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
ms.openlocfilehash: 0afdb02c578de92bc91c5f47e973148136ebd919
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892909"
---
# <a name="sql-server-launchpad-service-configuration"></a>Configuración del servicio Launchpad de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Otro [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio se crea para la instancia del motor de base de datos a la que se ha agregado la integración de SQL Server machine learning (R o Python).

## <a name="service-account-configuration"></a>Configuración de la cuenta de servicio

De forma predeterminada, Launchpad de SQL Server está configurado para ejecutarse bajo **NT Service\MSSQLLaunchpad**, que se aprovisiona con todos los permisos necesarios para ejecutar scripts externos. Eliminación de los permisos de esta cuenta puede dar lugar a Launchpad no se pudo iniciar o para tener acceso a la instancia de SQL Server donde se deberían ejecutar scripts externos.

Permiso necesario para esta cuenta se enumeran a continuación. Si modifica la cuenta de servicio, asegúrese de usar el **directiva de seguridad Local** aplicación para incluir estos permisos:

+ Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)
+ Omitir la comprobación transversal (SeChangeNotifyPrivilege)
+ Iniciar sesión como servicio (SeServiceLogonRight)
+ Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)

Para más información sobre los permisos para ejecutar servicios de SQL Server, vea [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>Propiedades de configuración

1. Abra el [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md). 

2. Haga clic en Launchpad de SQL Server y seleccione **propiedades**.

    + Para cambiar la cuenta de servicio, haga clic en el **iniciar sesión** ficha.

    + Para aumentar el número de usuarios, haga clic en el **avanzadas** ficha.

> [!Note]
> En las primeras versiones de SQL Server 2016 R Services, puede cambiar algunas propiedades del servicio mediante la edición de la [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] archivo de configuración. Este archivo ya no se usa para cambiar las configuraciones. Administrador de configuración de SQL Server es el enfoque correcto para los cambios de configuración del servicio, como la cuenta de servicio y el número de usuarios.

#### <a name="debug-settings"></a>Configuración de depuración

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
