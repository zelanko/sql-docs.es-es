---
title: Instalar extensiones de lenguaje (Java) de SQL Server en Linux | Microsoft Docs
description: Obtenga información sobre cómo instalar extensiones de lenguaje (Java) de SQL Server en Red Hat, Ubuntu y SUSE.
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9231828263020c352700fda6a4a0a9953dd70760
ms.sourcegitcommit: 65ceea905030582f8d89e75e97758abf3b1f0bd6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2019
ms.locfileid: "67399939"
---
# <a name="install-sql-server-2019-language-extensions-java-on-linux"></a>Instalar extensiones de lenguaje SQL Server de 2019 (Java) en Linux

Extensiones de lenguaje son un complemento para el motor de base de datos. Aunque puede [instalar el motor de base de datos y extensiones de lenguaje simultáneamente](#install-all), es una práctica recomendada para instalar y configurar primero el motor de base de datos de SQL Server para que pueda resolver los problemas antes de agregar más componentes. 

Siga los pasos descritos en este artículo para instalar la extensión del lenguaje Java.

Ubicación del paquete para las extensiones de Java es en los repositorios de origen de SQL Server para Linux. Si ya ha configurado los repositorios de código fuente para la instalación del motor de base de datos, puede ejecutar el **mssql-server-extensibilidad-java** comandos de instalación con el mismo repositorio de registro del paquete.

Extensiones de lenguaje también se admite en los contenedores de Linux. No se proporciona contenedores creados previamente con las extensiones de lenguaje, pero puede crear uno de los contenedores de SQL Server mediante [una plantilla de ejemplo disponible en GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="uninstall-previous-ctp"></a>Desinstalación de CTP anterior

Ha cambiado la lista de paquetes a través de las versiones CTP más recientes, lo que resulta en menos de paquetes. Se recomienda desinstalar la versión de CTP 2.x para quitar todos los paquetes anteriores antes de instalar la versión de CTP 3.1. No se admite la instalación en paralelo de varias versiones.

### <a name="1-confirm-package-installation"></a>1. Confirmar la instalación del paquete

Es posible que desee comprobar la existencia de una instalación anterior como primer paso. Los siguientes archivos indican una instalación existente: checkinstallextensibility.sh, exthost, launchpad.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2. Desinstalar los paquetes anteriores de CTP 2.x

Desinstalar en el nivel más bajo del paquete. Cualquier paquete ascendente depende de un paquete de nivel inferior se desinstala automáticamente.

  + Para la integración de Java, quitar **mssql-server-extensibilidad-java**

Comandos para quitar paquetes aparecen en la tabla siguiente.

| Plataforma  | Comandos de eliminación de paquete | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove msssql-server-extensibility-java`|

### <a name="3-proceed-with-ctp-31-install"></a>3. Continuar con la instalación de CTP 3.1

Instalar en el nivel más alto de paquete con las instrucciones de este artículo para su sistema operativo.

Para cada conjunto de instrucciones de instalación, específicos del sistema operativo *más alto nivel de paquete* sea **ejemplo 1: instalación completa** para todo el conjunto de paquetes, o **ejemplo 2: instalación mínima**  el menor número de paquetes necesarios para realizar una instalación viable.

1. Ejecute los comandos de instalación con los administradores de paquetes y la sintaxis para la distribución de Linux: 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>Requisitos previos

+ Debe ser la versión de Linux [compatibles con SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), pero no incluye el motor de Docker. Las versiones admitidas incluyen:

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ Debe tener una herramienta para ejecutar comandos de T-SQL. Un editor de consultas es necesario para la validación y configuración posterior a la instalación. Se recomienda [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), una descarga gratuita que se ejecuta en Linux.

## <a name="package-list"></a>Lista de paquetes

En un dispositivo conectado a internet, los paquetes se descargan e instalan independientemente el motor de base de datos mediante el instalador de paquetes para cada sistema operativo. En la tabla siguiente se describe todos los paquetes disponibles.

| Nombre del paquete | Se aplica a | Descripción |
|--------------|----------|-------------|
|mssql-server-extensibility  | Todos los idiomas | Marco de extensibilidad que se utiliza para ejecutar código de Java. |
|mssql-server-extensibility-java | Java | Extensión de Java para la carga de un entorno de ejecución de Java. No hay ninguna bibliotecas adicionales o paquetes para Java. |

<a name="RHEL"></a>

## <a name="install-language-extensions"></a>Instalar las extensiones de lenguaje

Puede instalar las extensiones de lenguaje y Java en Linux mediante la instalación **mssql-server-extensibilidad-java**. Al instalar **mssql-server-extensibilidad-java**, el paquete instala automáticamente el JRE 8 si ya no está instalado. También agregará la ruta de acceso JVM para una variable de entorno denominada variable.

> [!Note]
> En un servidor conectado a internet, las dependencias del paquete se descargó e instaladas como parte de la instalación del paquete principal. Si el servidor no está conectado a internet, consulte más detalles en el [el programa de instalación sin conexión](#offline-install).

### <a name="redhat-install-command"></a>Comando de instalación de Red Hat

Puede instalar las extensiones de lenguaje para Java en RedHat mediante el siguiente comando.

> [!Tip]
> Si es posible, ejecute `yum clean all` para actualizar paquetes en el sistema antes de la instalación.

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Comando de instalación de Ubuntu

Puede instalar las extensiones de lenguaje para Java en Ubuntu mediante el comando siguiente.

> [!Tip]
> Si es posible, ejecute `apt-get update` para actualizar paquetes en el sistema antes de la instalación. Además, algunas imágenes de docker de Ubuntu podrían no tener la opción de apt transporte https. Para instalarlo, utilice `apt-get install apt-transport-https`.

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>Comando de instalación SUSE

Puede instalar las extensiones de lenguaje para Java en SUSE mediante el comando siguiente.

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>Configuración posterior a la instalación (requerido)

1. Conceder permisos en Linux

    No es necesario realizar este paso si está utilizando bibliotecas externas. La manera recomendada de trabajo usa las bibliotecas externas. Para obtener ayuda acerca de la creación de una biblioteca externa desde el archivo jar, consulte [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)

    Si no usa bibliotecas externas, deberá proporcionar a SQL Server con permisos para ejecutar las clases de Java en su archivo jar.

    Para conceder la lectura y acceso de ejecución a un archivo jar, ejecute el siguiente **chmod** comando en el archivo jar. Se recomienda colocar siempre los archivos de clase en un archivo jar cuando se trabaja con SQL Server. Para obtener ayuda acerca de la creación de un archivo jar, consulte [cómo crear un archivo jar](https://docs.microsoft.com/sql/language-extensions/how-to/create-a-java-jar-file-from-class-files).

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    También deberá conceder permisos de mssql_satellite el archivo jar para lectura y ejecución.

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    Configuración adicional es principalmente a través del [herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).

2. Agregue la cuenta de usuario de mssql usada para ejecutar el servicio de SQL Server. Esto es necesario si no ha ejecutado el programa de instalación anteriormente.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. Habilitar el acceso de red saliente. Acceso de red saliente está deshabilitada de forma predeterminada. Para habilitar las solicitudes salientes, establezca el "outboundnetworkaccess" propiedad Boolean mediante la herramienta mssql-conf. Para obtener más información, consulte [configurar SQL Server en Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. Reinicie el servicio Launchpad de SQL Server y la instancia del motor de base de datos para leer los valores actualizados en el archivo INI. Un mensaje de reinicio le recuerda que cada vez que se modifica una configuración de extensibilidad.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. Habilitar la ejecución del script externo mediante Azure Data Studio u otra herramienta como SQL Server Management Studio (solo Windows) que ejecuta Transact-SQL.

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. Reinicie el `mssql-launchpadd` service de nuevo.

7. Para cada base de datos que desea usar en las extensiones de lenguaje, deberá registrar el lenguaje externo con [crear LENGUAJE externo](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql).

## <a name="register-external-language"></a>Registrar lenguaje externo

Para cada base de datos que desea usar en las extensiones de lenguaje, deberá registrar el lenguaje externo con [crear LENGUAJE externo](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql).

El ejemplo siguiente agrega un lenguaje externo llamado Java para una base de datos en SQL Server en Linux.

```SQL
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'<path-to-tar.gz>', FILE_NAME = 'javaextension.so');
GO
```

Para obtener más información, consulte [crear LENGUAJE externo](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql).

## <a name="verify-installation"></a>Comprobar la instalación

Característica de integración de Java no incluye las bibliotecas, pero puede ejecutar `grep -r JRE_HOME /etc` para confirmar la creación de la variable de entorno JAVA_HOME.

Para validar la instalación, ejecute un script de Transact-SQL que se ejecuta un sistema Java de invocación de procedimiento almacenado. Necesitará una herramienta de consulta para esta tarea. Azure Data Studio es una buena elección. Otras herramientas utilizadas habitualmente, como SQL Server Management Studio o PowerShell sólo Windows. Si tiene un equipo Windows con estas herramientas, puede usar para conectarse a la instalación de Linux del motor de base de datos.

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-language-extensions"></a>Instalación completa de SQL Server y extensiones de lenguaje

Puede instalar y configurar el motor de base de datos y extensiones de lenguaje en un procedimiento mediante la anexión de paquetes de Java y los parámetros en un comando que instala el motor de base de datos.

1. Proporcionar una línea de comandos que incluye el motor de base de datos, además de características de extensión del lenguaje.

  Puede agregar Java instalar extensibilidad a un motor de base de datos.

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

3. Acepte los contratos de licencia y completar la configuración posterior a la instalación. Use la **mssql-conf** herramienta para esta tarea.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  Se le pedirá que acepte el contrato de licencia para el motor de base de datos, elija una edición y establecer la contraseña de administrador. 

4. Reinicie el servicio, si se le pide que lo haga.

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>Instalación desatendida

Mediante el [instalación desatendida](https://docs.microsoft.com/sql/linux/sql-server-linux-setup#unattended) para el motor de base de datos, agregue los paquetes para mssql-server-extensibilidad-java.

<a name="offline-install"></a>


## <a name="offline-installation"></a>Instalación sin conexión

Siga el [instalación sin conexión](sql-server-linux-setup.md#offline) instrucciones para conocer los pasos sobre cómo instalar los paquetes. Busque el sitio de descarga y, a continuación, descargue los paquetes específicos mediante la siguiente lista de paquetes.

> [!Tip]
> Algunas de las herramientas de administración de paquetes proporcionan los comandos que pueden ayudarle a determinan las dependencias del paquete. Use yum, `sudo yum deplist [package]`. Para Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` seguido `dpkg -I [package name].deb`.

#### <a name="download-site"></a>Sitio de descarga

Puede descargar paquetes desde [ https://packages.microsoft.com/ ](https://packages.microsoft.com/). Todos los paquetes para Java se colocan con el paquete del motor de base de datos. 

#### <a name="redhat7-paths"></a>Rutas de acceso de Red Hat/7

|||
|--|----|
| extensibilidad/MSSQL-java paquetes | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |

#### <a name="ubuntu1604-paths"></a>Rutas de acceso de Ubuntu/16.04

|||
|--|----|
| extensibilidad/MSSQL-java paquetes | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |

#### <a name="suse12-paths"></a>Rutas de acceso SUSE/12

|||
|--|----|
| extensibilidad/MSSQL-java paquetes | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |

#### <a name="package-list"></a>Lista de paquetes

Dependiendo de las extensiones que desea usar, descargar los paquetes necesarios para un idioma específico. Los nombres de archivo exactos incluyen información de la plataforma en el sufijo, pero los siguientes nombres de archivo deben ser lo suficientemente cerca como para determinar qué archivos se deben obtener.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations-in-ctp-releases"></a>Limitaciones en las versiones CTP

Extensibilidad de extensiones de lenguaje y Java en Linux está todavía en desarrollo activo. Las siguientes características aún no están habilitadas en la versión preliminar.

+ Autenticación implícita no está disponible en Linux en este momento, lo que significa que no se puede conectar al servidor de Java en curso para obtener acceso a datos u otros recursos.


### <a name="resource-governance"></a>Regulación de recursos

Hay paridad entre Linux y Windows para [regulación de recursos](../t-sql/statements/create-external-resource-pool-transact-sql.md) para grupos de recursos externos, pero las estadísticas de [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) tienen actualmente unidades diferentes en Linux. Las unidades se alinearán en una próxima versión de CTP.
 
| Nombre de columna   | Descripción | Valor en Linux | 
|---------------|--------------|---------------|
|peak_memory_kb | La cantidad máxima de memoria usada para el grupo de recursos. | En Linux, esta estadística se origina del subsistema de memoria CGroups, donde el valor es memory.max_usage_in_bytes |
|write_io_count | El total de E/s de escritura emitidas desde que se restablecieron las estadísticas del regulador de recursos. | En Linux, esta estadística se origina desde el subsistema de blkio CGroups, donde el valor en la fila de escritura es blkio.throttle.io_serviced | 
|read_io_count | El total de E/s de lectura emitidas desde que se restablecieron las estadísticas del regulador de recursos. | En Linux, esta estadística se origina desde el subsistema de blkio CGroups, donde el valor de la fila de lectura es blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | El usuario kernel tiempo de CPU acumulado en milisegundos desde que se restablecieron las estadísticas del regulador de recursos. | En Linux, esta estadística se origina desde el subsistema de cpuacct CGroups, donde el valor en la fila del usuario es cpuacct.stat |  
|total_cpu_user_ms | El tiempo acumulado usuario de la CPU en milisegundos desde que se restablecieron las estadísticas del regulador de recursos.| En Linux, esta estadística se origina desde el subsistema de cpuacct CGroups, donde el valor en el valor de la fila del sistema es cpuacct.stat | 
|active_processes_count | El número de procesos externos que se ejecutan en el momento de la solicitud.| En Linux, esta estadística se origina desde el subsistema de PID GGroups, donde el valor es pids.current | 

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de Java pueden empezar a trabajar con algunos ejemplos sencillos y conozca los aspectos básicos del funcionamiento de Java con SQL Server. Para el siguiente paso, vea los siguientes vínculos:

+ [Tutorial: Expresiones regulares con Java](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)