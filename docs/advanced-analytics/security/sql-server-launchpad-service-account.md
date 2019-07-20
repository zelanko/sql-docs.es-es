---
title: Configuración de la cuenta de servicio de SQL Server Launchpad
description: Cómo modificar la cuenta de servicio de SQL Server Launchpad utilizada para la ejecución de scripts externos en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 9146020fb35d729575c8441e71b711e287399a75
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345526"
---
# <a name="sql-server-launchpad-service-configuration"></a>Configuración del servicio SQL Server Launchpad
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Es un servicio que administra y ejecuta scripts externos, de forma similar al modo en que el servicio de indización y consulta de texto completo inicia un host independiente para procesar las consultas de texto completo.

Para obtener más información, vea las secciones de Launchpad en la [arquitectura de extensibilidad en SQL Server Machine Learning Services](../../advanced-analytics/concepts/extensibility-framework.md#launchpad) y [la información general de seguridad para el marco de extensibilidad en SQL Server Machine Learning Services](../../advanced-analytics/concepts/security.md#launchpad).

## <a name="account-permissions"></a>Permisos de cuenta

De forma predeterminada, SQL Server Launchpad está configurado para ejecutarse en **NT Service\MSSQLLaunchpad**, que se aprovisiona con todos los permisos necesarios para ejecutar scripts externos. Si se quitan los permisos de esta cuenta, se producirá un error en el inicio de Launchpad o el acceso a la instancia de SQL Server donde se deben ejecutar los scripts externos.

Si modifica la cuenta de servicio, asegúrese de usar la [consola Directiva de seguridad local](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings).

En la tabla siguiente se muestran los permisos necesarios para esta cuenta.

| Configuración de directiva de grupo | Nombre de constante |
|----------------------|---------------|
| [Ajustar cuotas de memoria para un proceso](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/adjust-memory-quotas-for-a-process) | SeIncreaseQuotaPrivilege | 
| [Omitir comprobación de recorrido](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/bypass-traverse-checking) | SeChangeNotifyPrivilege | 
| [Iniciar sesión como servicio](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/log-on-as-a-service) | SeServiceLogonRight | 
| [Reemplazar un token de nivel de proceso](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/replace-a-process-level-token) | SeAssignPrimaryTokenPrivilege | 

Para más información sobre los permisos para ejecutar servicios de SQL Server, vea [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

<a name="bkmk_ChangingConfig"></a> 

## <a name="configuration-properties"></a>Propiedades de configuración

Normalmente, no hay ningún motivo para modificar la configuración del servicio. Las propiedades que se pueden cambiar son la cuenta de servicio, el número de procesos externos (20 de forma predeterminada) o la Directiva de restablecimiento de contraseña para las cuentas de trabajo.

1. Abra el [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md).

2. En servicios de SQL Server, haga clic con el botón secundario en SQL Server Launchpad y seleccione **propiedades**.
  + Para cambiar la cuenta de servicio, haga clic en la pestaña **iniciar sesión** .
  + Para aumentar el número de usuarios, haga clic en la pestaña **Opciones avanzadas** y cambie el número de contextos de **seguridad**.

> [!Note]
> En las primeras versiones de SQL Server 2016 R Services, podría cambiar algunas propiedades del servicio editando el [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] archivo de configuración. Este archivo ya no se utiliza para cambiar las configuraciones. Administrador de configuración de SQL Server es el enfoque adecuado para los cambios en la configuración del servicio, como la cuenta de servicio y el número de usuarios.

## <a name="debug-settings"></a>Configuración de depuración

Solo se pueden cambiar algunas propiedades mediante el archivo de configuración de Launchpad, que puede ser útil en casos limitados, como la depuración. El archivo de configuración se crea durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la instalación y, de forma predeterminada, se guarda como un `<instance path>\binn\rlauncher.config`archivo de texto sin formato en.

Para realizar cambios en este archivo, debe ser administrador en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si edita el archivo, se recomienda realizar una copia de seguridad antes de guardar los cambios.

En la tabla siguiente se muestra la configuración [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]avanzada de, con los valores permitidos.

|**Nombre de opción**|**Tipo**|**Descripción**|
|----|----|----|
|LIMPIEZA\_\_DETRABAJOALSALIR\_|Entero |Esta es solo una configuración interna: no cambie este valor. </br></br>Especifica si se debe limpiar la carpeta de trabajo temporal creada para cada sesión de tiempo de ejecución externa una vez completada la sesión. Esta opción resulta útil para la depuración. </br></br>Los valores admitidos son **0** (deshabilitado) o **1** (habilitado). </br></br>El valor predeterminado es 1, lo que significa que los archivos de registro se quitan al salir.|
|NIVEL\_DE SEGUIMIENTO|Entero |Configura el nivel de detalle de seguimiento de MSSQLLAUNCHPAD para fines de depuración. Esto afecta a los archivos de seguimiento de la ruta de acceso especificada por la configuración LOG_DIRECTORY. </br></br>Los valores admitidos son: **1** (error), **2** (rendimiento), **3** (ADVERTENCIA), **4** (información). </br></br>El valor predeterminado es 1, lo que significa que solo se producen errores de salida.|

Todas las opciones se presentan como un par clave-valor y cada una de ellas se encuentra en una línea aparte. Por ejemplo, para cambiar el nivel de seguimiento, debe agregar la línea `Default: TRACE_LEVEL=4`.

<a name="bkmk_EnforcePolicy"></a>

## <a name="enforcing-password-policy"></a>Aplicación de la Directiva de contraseñas

Si su organización tiene una directiva que requiere el cambio de contraseñas de forma periódica, podría tener que forzar el servicio Launchpad para que regenere las contraseñas cifradas que Launchpad conserva para sus cuentas de trabajo.

Para habilitar esta opción de configuración y forzar la actualización de las contraseñas, abra el panel **Propiedades** del servicio Launchpad en el Administrador de configuración de SQL Server, haga clic en **Avanzado** y cambie **Restablecer contraseña de usuarios externos** a **Sí**. Al aplicar este cambio, las contraseñas se regenerarán inmediatamente para todas las cuentas de usuario. Para ejecutar un script externo después de este cambio, debe reiniciar el servicio Launchpad, momento en el que se leerán las contraseñas recién generadas.

Para restablecer las contraseñas a intervalos regulares, puede establecer esta marca manualmente o usar un script.

## <a name="next-steps"></a>Pasos siguientes

+ [Marco de extensibilidad](../concepts/extensibility-framework.md)
+ [Información general sobre seguridad](../concepts/security.md)
