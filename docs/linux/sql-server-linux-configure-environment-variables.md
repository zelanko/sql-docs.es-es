---
title: "Configuración de SQL Server con las variables de entorno | Documentos de Microsoft"
description: "En este tema se describe cómo usar variables de entorno para configurar valores específicos de 2017 de SQL Server en Linux."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/21/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 4951f503a7b5c395f86cb6daf2ba705ca69fbd83
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="configure-sql-server-settings-with-environment-variables-on-linux"></a>Configuración de SQL Server con las variables de entorno en Linux

Puede utilizar varias variables de entorno diferente para configurar SQL Server de 2017 RC2 en Linux. Estas variables se utilizan en dos escenarios:

- Para configurar la instalación inicial con el `mssql-conf setup` comando.
- Para configurar una nueva [contenedor de SQL Server en Docker](quickstart-install-connect-docker.md).

> [!TIP]
> Si tiene que configurar SQL Server después de estos escenarios de instalación, consulte [configurar SQL Server en Linux con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).

## <a name="environment-variables"></a>Variables de entorno

| Variable de entorno | Description |
|-----|-----|
| **ACCEPT_EULA** | Acepte el contrato de licencia de SQL Server cuando se establece en cualquier valor (por ejemplo, ' Y'). |
| **MSSQL_SA_PASSWORD** | Configurar la contraseña del usuario administrador. |
| **MSSQL_PID** | Establecer la clave de producto o de edición de SQL Server. Los valores posibles incluyen: Evaluation, Developer, Express, Web, Standard, Enterprise o una clave de producto en el formulario de ###-###-###-###-###, donde '#' es una letra o un número. |
| **MSSQL_LCID** | Establece el identificador de idioma que se usará para SQL Server. Por ejemplo, 1036 es francés. |
| **MSSQL_COLLATION** | Establece la intercalación predeterminada de SQL Server. Esto invalida la asignación predeterminada de identificador de idioma (LCID) a la intercalación. |
| **MSSQL_MEMORY_LIMIT_MB** | Establece la cantidad máxima de memoria (en MB) que puede utilizar SQL Server. De forma predeterminada es el 80% de la memoria física total. |
| **MSSQL_TCP_PORT** | Configurar el puerto TCP que SQL Server escucha en (predeterminado: 1433). |
| **MSSQL_IP_ADDRESS** | Establecer la dirección IP. Actualmente, la dirección IP debe ser IPv4 estilo (0.0.0.0). |
| **MSSQL_BACKUP_DIR** | Establecer la ubicación del directorio de copia de seguridad de forma predeterminada. |
| **MSSQL_DATA_DIR** | Cambie el directorio donde se crean los nuevos archivos de datos de base de datos de SQL Server (.mdf). |
| **MSSQL_LOG_DIR** | Cambie el directorio donde se crean los nuevos archivos de registro (.ldf) de la base de datos de SQL Server. |
| **MSSQL_DUMP_DIR** | Cambie el directorio donde SQL Server se deposite los volcados de memoria y otros archivos de solución de problemas de forma predeterminada. |
| **MSSQL_ENABLE_HADR** | Habilite los grupos de disponibilidad. |

## <a name="example-initial-setup"></a>Ejemplo: el programa de instalación inicial

En este ejemplo se ejecuta `mssql-conf setup` con configura las variables de entorno. Se especifican las variables de entorno siguientes:

- **ACCEPT_EULA** acepta el contrato de licencia de usuario final.
- **MSSSQL_PID** especifica la libremente con licencia Developer Edition de SQL Server para su uso no es de producción.
- **MSSQL_SA_PASSWORD** establece una contraseña segura.
- **MSSQL_TCP_PORT** establece el puerto TCP que SQL Server escucha en 1234.

```bash
sudo ACCEPT_EULA='Y' MSSQL_PID='Developer' MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' MSSQL_TCP_PORT=1234 /opt/mssql/bin/mssql-conf setup
```

## <a name="example-docker"></a>Ejemplo: Docker

Este comando de docker de ejemplo utiliza las siguientes variables de entorno para crear un nuevo contenedor de 2017 de SQL Server:

- **ACCEPT_EULA** acepta el contrato de licencia de usuario final.
- **MSSSQL_PID** especifica la libremente con licencia Developer Edition de SQL Server para su uso no es de producción.
- **MSSQL_SA_PASSWORD** establece una contraseña segura.
- **MSSQL_TCP_PORT** establece el puerto TCP que SQL Server escucha en 1234. Esto significa que en lugar de puerto de asignación 1433 (valor predeterminado) a un puerto de host, debe asignar el puerto TCP personalizado con el `-p 1234:1234` en este ejemplo.

Si está ejecutando Docker en Linux/macOS, use la siguiente sintaxis con comillas simples:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID='Developer' -e MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' -e MSSQL_TCP_PORT=1234 --cap-add SYS_PTRACE -p 1234:1234 -d microsoft/mssql-server-linux
```

Si está ejecutando Docker en Windows, utilice la siguiente sintaxis con comillas dobles:

```bash
docker run -e ACCEPT_EULA=Y -e MSSQL_PID="Developer" -e MSSQL_SA_PASSWORD="<YourStrong!Passw0rd>" -e MSSQL_TCP_PORT=1234 --cap-add SYS_PTRACE -p 1234:1234 -d microsoft/mssql-server-linux
```

## <a name="next-steps"></a>Pasos siguientes

Para otras configuraciones de SQL Server no aparece aquí, consulte [configurar SQL Server en Linux con la herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).

Para obtener más información acerca de cómo instalar y ejecutar SQL Server en Linux, consulte [instalar SQL Server en Linux](sql-server-linux-setup.md).

