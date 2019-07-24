---
title: Configurar los valores de SQL Server con variables de entorno
description: En este artículo se describe cómo usar variables de entorno para configurar opciones específicas de SQL Server 2017 en Linux.
author: VanMSFT
ms.author: vanto
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 51589a2183043c5c8ea8d1f9bf5d4af6fcc1eea3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419247"
---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Configuración de SQL Server con variables de entorno en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Puede usar varias variables de entorno diferentes para configurar SQL Server 2017 en Linux. Estas variables se usan en dos escenarios:

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Puede usar varias variables de entorno diferentes para configurar SQL Server versión preliminar 2019 en Linux. Estas variables se usan en dos escenarios:

::: moniker-end

- Para configurar la instalación inicial con `mssql-conf setup` el comando.
- Para configurar un nuevo [contenedor de SQL Server en Docker](quickstart-install-connect-docker.md).

> [!TIP]
> Si necesita configurar SQL Server después de estos escenarios de instalación, consulte [configuración de SQL Server en Linux con la herramienta MSSQL-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="environment-variables"></a>Variables de entorno

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

| Variable de entorno | Descripción |
|-----|-----|
| **ACCEPT_EULA** | Establezca la variable **ACCEPT_EULA** en cualquier valor para confirmar que acepta el [Contrato de licencia de usuario final](https://go.microsoft.com/fwlink/?LinkId=746388). Configuración requerida para la imagen de SQL Server. |
| **MSSQL_SA_PASSWORD** | Configure la contraseña de usuario SA. |
| **MSSQL_PID** | Establezca la edición de SQL Server o la clave de producto. Los valores posibles incluyen: </br></br>**Evaluation**</br>**Desarrollador**</br>**Express**</br>**Web**</br>**Estándar**</br>**Enterprise**</br>**Una clave de producto**</br></br>Si se especifica una clave de producto, debe tener el formato # # # # #-# # # # #-# # # # #-# # # # #-# # # # #, donde "#" es un número o una letra.|
| **MSSQL_LCID** | Establece el identificador de idioma que se va a usar para SQL Server. Por ejemplo 1036 es francés. |
| **MSSQL_COLLATION** | Establece la intercalación predeterminada para SQL Server. Esto invalida la asignación predeterminada de identificador de idioma (LCID) a la intercalación. |
| **MSSQL_MEMORY_LIMIT_MB** | Establece la cantidad máxima de memoria (en MB) que SQL Server puede usar. De forma predeterminada, es el 80% de la memoria física total. |
| **MSSQL_TCP_PORT** | Configure el puerto TCP en el que escucha SQL Server (valor predeterminado 1433). |
| **MSSQL_IP_ADDRESS** | Establezca la dirección IP. Actualmente, la dirección IP debe ser el estilo IPv4 (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Establezca la ubicación predeterminada del directorio de copia de seguridad. |
| **MSSQL_DATA_DIR** | Cambiar el directorio en el que se crean los archivos de datos de la base de datos de SQL Server nuevos (. MDF). |
| **MSSQL_LOG_DIR** | Cambie el directorio en el que se crean los nuevos archivos de registro de la base de datos de SQL Server (. ldf). |
| **MSSQL_DUMP_DIR** | Cambie el directorio en el que SQL Server depositará los volcados de memoria y otros archivos de solución de problemas de forma predeterminada. |
| **MSSQL_ENABLE_HADR** | Habilite el grupo de disponibilidad. Por ejemplo, ' 1 ' está habilitado y ' 0 ' está deshabilitado |
| **MSSQL_AGENT_ENABLED** | Habilitar Agente SQL Server. Por ejemplo, ' true ' está habilitado y ' false ' está deshabilitado. De forma predeterminada, el agente está deshabilitado.  |
| **MSSQL_MASTER_DATA_FILE** | Establece la ubicación del archivo de datos de la base de datos maestra. Se debe llamar **Master. MDF** hasta la primera ejecución de SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Establece la ubicación del archivo de registro de la base de datos maestra. Debe denominarse **mastlog. ldf** hasta la primera ejecución de SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Establece la ubicación de los archivos ErrorLog. |

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

| Variable de entorno | Descripción |
|-----|-----|
| **ACCEPT_EULA** | Establezca la variable **ACCEPT_EULA** en cualquier valor para confirmar que acepta el [Contrato de licencia de usuario final](https://go.microsoft.com/fwlink/?LinkId=746388). Configuración requerida para la imagen de SQL Server. |
| **MSSQL_SA_PASSWORD** | Configure la contraseña de usuario SA. |
| **MSSQL_PID** | Establezca la edición de SQL Server o la clave de producto. Los valores posibles incluyen: </br></br>**Evaluation**</br>**Desarrollador**</br>**Express**</br>**Web**</br>**Estándar**</br>**Enterprise**</br>**Una clave de producto**</br></br>Si se especifica una clave de producto, debe tener el formato # # # # #-# # # # #-# # # # #-# # # # #-# # # # #, donde "#" es un número o una letra.|
| **MSSQL_LCID** | Establece el identificador de idioma que se va a usar para SQL Server. Por ejemplo 1036 es francés. |
| **MSSQL_COLLATION** | Establece la intercalación predeterminada para SQL Server. Esto invalida la asignación predeterminada de identificador de idioma (LCID) a la intercalación. |
| **MSSQL_MEMORY_LIMIT_MB** | Establece la cantidad máxima de memoria (en MB) que SQL Server puede usar. De forma predeterminada, es el 80% de la memoria física total. |
| **MSSQL_TCP_PORT** | Configure el puerto TCP en el que escucha SQL Server (valor predeterminado 1433). |
| **MSSQL_IP_ADDRESS** | Establezca la dirección IP. Actualmente, la dirección IP debe ser el estilo IPv4 (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Establezca la ubicación predeterminada del directorio de copia de seguridad. |
| **MSSQL_DATA_DIR** | Cambiar el directorio en el que se crean los archivos de datos de la base de datos de SQL Server nuevos (. MDF). |
| **MSSQL_LOG_DIR** | Cambie el directorio en el que se crean los nuevos archivos de registro de la base de datos de SQL Server (. ldf). |
| **MSSQL_DUMP_DIR** | Cambie el directorio en el que SQL Server depositará los volcados de memoria y otros archivos de solución de problemas de forma predeterminada. |
| **MSSQL_ENABLE_HADR** | Habilite el grupo de disponibilidad. Por ejemplo, ' 1 ' está habilitado y ' 0 ' está deshabilitado |
| **MSSQL_AGENT_ENABLED** | Habilitar Agente SQL Server. Por ejemplo, ' true ' está habilitado y ' false ' está deshabilitado. De forma predeterminada, el agente está deshabilitado.  |
| **MSSQL_MASTER_DATA_FILE** | Establece la ubicación del archivo de datos de la base de datos maestra. Se debe llamar **Master. MDF** hasta la primera ejecución de SQL Server. |
| **MSSQL_MASTER_LOG_FILE** | Establece la ubicación del archivo de registro de la base de datos maestra. Debe denominarse **mastlog. ldf** hasta la primera ejecución de SQL Server. |
| **MSSQL_ERROR_LOG_FILE** | Establece la ubicación de los archivos ErrorLog. |

::: moniker-end

## <a name="use-with-initial-setup"></a>Usar con la configuración inicial

Este ejemplo se `mssql-conf setup` ejecuta con variables de entorno configuradas. Se especifican las siguientes variables de entorno:

- **ACCEPT_EULA** acepta el contrato de licencia para el usuario final.
- **MSSSQL_PID** especifica la edición para desarrolladores con licencia gratuita de SQL Server para su uso no en producción.
- **MSSQL_SA_PASSWORD** establece una contraseña segura.
- **MSSQL_TCP_PORT** establece el puerto TCP en el que SQL Server escucha en 1234.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="use-with-docker"></a>Uso con Docker

Este comando de Docker de ejemplo usa las siguientes variables de entorno para crear un nuevo contenedor de SQL Server:

- **ACCEPT_EULA** acepta el contrato de licencia para el usuario final.
- **MSSSQL_PID** especifica la edición para desarrolladores con licencia gratuita de SQL Server para su uso no en producción.
- **MSSQL_SA_PASSWORD** establece una contraseña segura.
- **MSSQL_TCP_PORT** establece el puerto TCP en el que SQL Server escucha en 1234. Esto significa que, en lugar de asignar el puerto 1433 (predeterminado) a un puerto de host, el puerto TCP personalizado se debe `-p 1234:1234` asignar con el comando en este ejemplo.

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Si ejecuta Docker en Linux/macOS, use la siguiente sintaxis con comillas simples:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

Si ejecuta Docker en Windows, use la siguiente sintaxis con comillas dobles:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2017-latest
```

> [!NOTE]
> El proceso para ejecutar las ediciones de producción en contenedores es ligeramente diferente. Para obtener más información, vea [Run production container image](sql-server-linux-configure-docker.md#production) (Ejecutar imágenes de contenedor de producción).

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Si ejecuta Docker en Linux/macOS, use la siguiente sintaxis con comillas simples:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

Si ejecuta Docker en Windows, use la siguiente sintaxis con comillas dobles:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 -p 1234:1234 -d mcr.microsoft.com/mssql/server:2019-CTP3.1-ubuntu
```

::: moniker-end

## <a name="next-steps"></a>Pasos siguientes

Para ver otras opciones de SQL Server que no se muestran aquí, consulte [configuración de SQL Server en Linux con la herramienta MSSQL-conf](sql-server-linux-configure-mssql-conf.md).

Para obtener más información sobre cómo instalar y ejecutar SQL Server en Linux, consulte [instalar SQL Server en Linux](sql-server-linux-setup.md).
