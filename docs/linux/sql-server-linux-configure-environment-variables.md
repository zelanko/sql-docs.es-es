---
title: Configurar la configuración de SQL Server con las variables de entorno | Microsoft Docs
description: En este artículo se describe cómo usar variables de entorno para configurar valores específicos de SQL Server 2017 en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 87e4d1ed1bdb1ce78e2f45fcb49019175fcdfefd
ms.sourcegitcommit: a2be75158491535c9a59583c51890e3457dc75d6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2018
ms.locfileid: "51269698"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Configurar la configuración de SQL Server con las variables de entorno en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Puede utilizar varias variables de entorno diferentes para configurar SQL Server 2017 en Linux. Estas variables se usan en dos escenarios:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Puede utilizar varias variables de entorno diferentes para configurar la versión preliminar de SQL Server 2019 en Linux. Estas variables se usan en dos escenarios:

::: moniker-end

- Para configurar la instalación inicial con el `mssql-conf setup` comando.
- Para configurar una nueva [contenedor de SQL Server en Docker](quickstart-install-connect-docker.md).

> [!TIP]
> Si tiene que configurar SQL Server después de estos escenarios de instalación, consulte [configurar SQL Server en Linux con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="environment-variables"></a>Variables de entorno

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| Variable de entorno | Descripción |
|-----|-----|
| **ACCEPT_EULA** | Acepte el contrato de licencia de SQL Server cuando se establece en cualquier valor (por ejemplo, ' Y'). |
| **MSSQL_SA_PASSWORD** | Configurar la contraseña del usuario SA. |
| **MSSQL_PID** | Establezca la clave de producto o la edición de SQL Server. Los valores posibles incluyen: </br></br>**Evaluation**</br>**Desarrollador**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Una clave de producto**</br></br>Si especifica una clave de producto, debe ser en forma de ###-###-###-###-###, donde '#' es un número o una letra.|
| **MSSQL_LCID** | Establece el identificador de idioma que se usará para SQL Server. Por ejemplo, 1036 es francés. |
| **MSSQL_COLLATION** | Establece la intercalación predeterminada de SQL Server. Esto invalida la asignación predeterminada de Id. de idioma (LCID) a la intercalación. |
| **MSSQL_MEMORY_LIMIT_MB** | Establece la cantidad máxima de memoria (en MB) que puede usar SQL Server. De forma predeterminada es el 80% de la memoria física total. |
| **MSSQL_TCP_PORT** | Configure el puerto TCP que SQL Server escucha en (predeterminado: 1433). |
| **MSSQL_IP_ADDRESS** | Establecer la dirección IP. Actualmente, la dirección IP debe ser IPv4 estilo (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Establecer la ubicación del directorio de copia de seguridad predeterminada. |
| **MSSQL_DATA_DIR** | Cambie el directorio donde se crean los nuevos archivos de datos de base de datos de SQL Server (.mdf). |
| **MSSQL_LOG_DIR** | Cambie el directorio donde se crean los nuevos archivos de registro (.ldf) de base de datos de SQL Server. |
| **MSSQL_DUMP_DIR** | Cambie el directorio donde SQL Server se deposita los volcados de memoria y otros archivos de solución de problemas de forma predeterminada. |
| **MSSQL_ENABLE_HADR** | Habilitar grupo de disponibilidad. Por ejemplo, '1' está habilitada, y está deshabilitado '0' |
| **MSSQL_AGENT_ENABLED** | Habilitar el Agente SQL Server. Por ejemplo, está habilitado 'true' y 'false' está deshabilitado. De forma predeterminada, se deshabilita el agente.  |
| **MSSQL_MASTER_DATA_FILE** | Establece la ubicación del archivo de datos de base de datos maestra. Se debe denominar **master.mdf** hasta que se ejecuta por primera vez de SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Establece la ubicación del archivo de registro de base de datos maestra. Se debe denominar **mastlog.ldf** hasta que se ejecuta por primera vez de SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Establece la ubicación de los archivos de registro de errores. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| Variable de entorno | Descripción |
|-----|-----|
| **ACCEPT_EULA** | Acepte el contrato de licencia de SQL Server cuando se establece en cualquier valor (por ejemplo, ' Y'). |
| **MSSQL_SA_PASSWORD** | Configurar la contraseña del usuario SA. |
| **MSSQL_PID** | Establezca la clave de producto o la edición de SQL Server. Los valores posibles incluyen: </br></br>**Evaluation**</br>**Desarrollador**</br>**Express**</br>**Web**</br>**Standard**</br>**Enterprise**</br>**Una clave de producto**</br></br>Si especifica una clave de producto, debe ser en forma de ###-###-###-###-###, donde '#' es un número o una letra.|
| **MSSQL_LCID** | Establece el identificador de idioma que se usará para SQL Server. Por ejemplo, 1036 es francés. |
| **MSSQL_COLLATION** | Establece la intercalación predeterminada de SQL Server. Esto invalida la asignación predeterminada de Id. de idioma (LCID) a la intercalación. |
| **MSSQL_MEMORY_LIMIT_MB** | Establece la cantidad máxima de memoria (en MB) que puede usar SQL Server. De forma predeterminada es el 80% de la memoria física total. |
| **MSSQL_TCP_PORT** | Configure el puerto TCP que SQL Server escucha en (predeterminado: 1433). |
| **MSSQL_IP_ADDRESS** | Establecer la dirección IP. Actualmente, la dirección IP debe ser IPv4 estilo (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Establecer la ubicación del directorio de copia de seguridad predeterminada. |
| **MSSQL_DATA_DIR** | Cambie el directorio donde se crean los nuevos archivos de datos de base de datos de SQL Server (.mdf). |
| **MSSQL_LOG_DIR** | Cambie el directorio donde se crean los nuevos archivos de registro (.ldf) de base de datos de SQL Server. |
| **MSSQL_DUMP_DIR** | Cambie el directorio donde SQL Server se deposita los volcados de memoria y otros archivos de solución de problemas de forma predeterminada. |
| **MSSQL_ENABLE_HADR** | Habilitar grupo de disponibilidad. Por ejemplo, '1' está habilitada, y está deshabilitado '0' |
| **MSSQL_AGENT_ENABLED** | Habilitar el Agente SQL Server. Por ejemplo, está habilitado 'true' y 'false' está deshabilitado. De forma predeterminada, se deshabilita el agente.  |
| **MSSQL_MASTER_DATA_FILE** | Establece la ubicación del archivo de datos de base de datos maestra. Se debe denominar **master.mdf** hasta que se ejecuta por primera vez de SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Establece la ubicación del archivo de registro de base de datos maestra. Se debe denominar **mastlog.ldf** hasta que se ejecuta por primera vez de SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Establece la ubicación de los archivos de registro de errores. |

::: moniker-end

## <a name="use-with-initial-setup"></a>Usar con la instalación inicial

Este ejemplo se ejecuta `mssql-conf setup` con configura las variables de entorno. Se especifican las variables de entorno siguientes:

- **ACCEPT_EULA** acepta el contrato de licencia de usuario final.
- **MSSSQL_PID** especifica la licencia libre Developer Edition de SQL Server para su uso que no sea de producción.
- **MSSQL_SA_PASSWORD** establece una contraseña segura.
- **MSSQL_TCP_PORT** establece el puerto TCP que SQL Server escucha en 1234.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>Uso con Docker

Este comando de docker de ejemplo usa las siguientes variables de entorno para crear un nuevo contenedor de SQL Server:

- **ACCEPT_EULA** acepta el contrato de licencia de usuario final.
- **MSSSQL_PID** especifica la licencia libre Developer Edition de SQL Server para su uso que no sea de producción.
- **MSSQL_SA_PASSWORD** establece una contraseña segura.
- **MSSQL_TCP_PORT** establece el puerto TCP que SQL Server escucha en 1234. Esto significa que en lugar del puerto 1433 (predeterminado) de asignación a un puerto de host, se debe asignar el puerto TCP personalizado con el `-p 1234:1234` comando en este ejemplo.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Si está ejecutando Docker en Linux y macOS, use la siguiente sintaxis con comillas simples:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

Si está ejecutando Docker en Windows, utilice la siguiente sintaxis con comillas dobles:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

> [!NOTE]
> El proceso para ejecutar las ediciones de producción en contenedores es ligeramente diferente. Para obtener más información, vea [Run production container image](sql-server-linux-configure-docker.md#production) (Ejecutar imágenes de contenedor de producción).

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Si está ejecutando Docker en Linux y macOS, use la siguiente sintaxis con comillas simples:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

Si está ejecutando Docker en Windows, utilice la siguiente sintaxis con comillas dobles:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:vNext-CTP2.0-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>Pasos siguientes

Para otras configuraciones de SQL Server no aparece aquí, consulte [configurar SQL Server en Linux con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).

Para obtener más información sobre cómo instalar y ejecutar SQL Server en Linux, consulte [instalar SQL Server en Linux](sql-server-linux-setup.md).
