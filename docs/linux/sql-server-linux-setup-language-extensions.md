---
title: Instalación de Extensiones de lenguaje (Java) de SQL Server en Linux
description: Aprenda a instalar Extensiones de lenguaje (Java) de SQL Server en Red Hat, Ubuntu y SUSE.
author: dphansen
ms.author: davidph
ms.reviewer: vanto
manager: cgronlun
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: de5ca4f46513999c1473eed77503b59cc94c3a22
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68476020"
---
# <a name="install-sql-server-2019-language-extensions-java-on-linux"></a>Instalación de Extensiones de lenguaje (Java) de SQL Server 2019 en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Extensiones de lenguaje es un complemento del motor de base de datos. Aunque puede [instalar el motor de base de datos y Extensiones de lenguaje de forma simultánea](#install-all), el procedimiento recomendado es instalar y configurar primero el motor de base de datos de SQL Server para poder resolver cualquier problema antes de agregar más componentes. 

Siga los pasos de este artículo para instalar la extensión de lenguaje Java.

La ubicación del paquete de las extensiones de Java está en los repositorios de origen de Linux para SQL Server. Si ya ha configurado repositorios de origen para la instalación del motor de base de datos, puede ejecutar los comandos de instalación del paquete **mssql-server-extensibility-java** mediante el mismo registro de repositorio.

Extensiones de lenguaje también se admite en contenedores de Linux. No se proporcionan contenedores preintegrados con Extensiones de lenguaje, pero puede crear uno a partir de los contenedores de SQL Server mediante [una plantilla de ejemplo disponible en GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="uninstall-previous-ctp"></a>Desinstalación de una CTP anterior

La lista de paquetes ha cambiado con las últimas versiones CTP, lo que ha dado lugar a menos paquetes. Antes de instalar CTP 3.2, se recomienda desinstalar CTP 2.x para quitar todos los paquetes anteriores. La instalación en paralelo de varias versiones no se admite.

### <a name="1-confirm-package-installation"></a>1. Confirmación de la instalación del paquete

Es posible que quiera comprobar la existencia de una instalación anterior como primer paso. Los archivos siguientes indican una instalación existente: checkinstallextensibility.sh, exthost, launchpad.

```bash
ls /opt/microsoft/mssql/bin
```

### <a name="2-uninstall-previous-ctp-2x-packages"></a>2. Desinstalación de paquetes anteriores de CTP 2.x

Desinstale en el nivel de paquete inferior. Los paquetes superiores que dependen de un paquete de nivel inferior se desinstalan automáticamente.

  + Para la integración de Java, quite **mssql-server-extensibility-java**

Los comandos para quitar paquetes aparecen en la tabla siguiente.

| Plataforma  | Comandos de eliminación de paquetes | 
|-----------|----------------------------|
| RHEL  | `sudo yum remove msssql-server-extensibility-java` |
| SLES  | `sudo zypper remove msssql-server-extensibility-java` |
| Ubuntu    | `sudo apt-get remove msssql-server-extensibility-java`|

### <a name="3-proceed-with-ctp-32-install"></a>3. Continuar con la instalación de CTP 3.2

Instale en el nivel de paquete superior con las instrucciones de este artículo para el sistema operativo.

Para cada conjunto específico de un sistema operativo de instrucciones de instalación, el  *nivel de paquete superior* es **Ejemplo 1: instalación completa** para el conjunto completo de paquetes o **Ejemplo 2: instalación mínima** para el número mínimo de paquetes necesario para una instalación viable.

1. Ejecute los comandos de instalación mediante los administradores de paquetes y la sintaxis de la distribución de Linux: 

   + [RedHat](#RHEL)
   + [Ubuntu](#ubuntu)
   + [SUSE](#suse)

## <a name="prerequisites"></a>Prerequisites

+ La versión de Linux debe ser [compatible con SQL Server](sql-server-linux-release-notes-2019.md#supported-platforms), pero no incluye el motor de Docker. Las versiones admitidas incluyen:

   + [Red Hat Enterprise Linux (RHEL)](quickstart-install-connect-red-hat.md)

   + [SUSE Enterprise Linux Server](quickstart-install-connect-suse.md)

   + [Ubuntu](quickstart-install-connect-ubuntu.md)

+ Debe tener una herramienta para ejecutar comandos de T-SQL. Se necesita un editor de consultas para la configuración y la validación posteriores a la instalación. Se recomienda [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download?view=sql-server-2017#get-azure-data-studio-for-linux), una descarga gratuita que se ejecuta en Linux.

## <a name="package-list"></a>Lista de paquetes

En un dispositivo conectado a Internet, los paquetes se descargan e instalan de forma independiente del motor de base de datos mediante el instalador de paquetes de cada sistema operativo. En la tabla siguiente se indican todos los paquetes disponibles.

| Nombre del paquete | Se aplica a | Descripción |
|--------------|----------|-------------|
|mssql-server-extensibility  | Todos los idiomas | Marco de extensibilidad que se usa para ejecutar código Java. |
|mssql-server-extensibility-java | Java | Extensión de Java para cargar un entorno de ejecución de Java. No hay bibliotecas ni paquetes adicionales para Java. |

<a name="RHEL"></a>

## <a name="install-language-extensions"></a>Instalación de Extensiones de lenguaje

Puede instalar Extensiones de lenguaje y Java en Linux si instala **mssql-server-extensibility-java**. Al instalar **mssql-server-extensibility-java**, el paquete instala automáticamente JRE 8 si aún no está instalado. También agrega la ruta de acceso de JVM a una variable de entorno denominada JRE_HOME.

> [!Note]
> En un servidor conectado a Internet, las dependencias de paquete se descargan e instalan como parte de la instalación del paquete principal. Si el servidor no está conectado a Internet, vea más detalles en la [instalación sin conexión](#offline-install).

### <a name="redhat-install-command"></a>Comando de instalación de RedHat

Puede instalar Extensiones de lenguaje para Java en RedHat con el siguiente comando.

> [!Tip]
> Si es posible, ejecute `yum clean all` para actualizar los paquetes en el sistema antes de la instalación.

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility-java
```

<a name="ubuntu"></a>

### <a name="ubuntu-install-command"></a>Comando de instalación de Ubuntu

Puede instalar Extensiones de lenguaje para Java en Ubuntu con el siguiente comando.

> [!Tip]
> Si es posible, ejecute `apt-get update` para actualizar los paquetes en el sistema antes de la instalación. Además, algunas imágenes de Docker de Ubuntu podrían no tener la opción https apt transport. Para instalarla, use `apt-get install apt-transport-https`.

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility-java
```

<a name="suse"></a>

### <a name="suse-install-command"></a>Comando de instalación de SUSE

Puede instalar Extensiones de lenguaje para Java en SUSE con el siguiente comando.

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility-java
```

## <a name="post-install-config-required"></a>Configuración posterior a la instalación (obligatoria)

1. Conceda permisos en Linux

    No es necesario realizar este paso si se usan bibliotecas externas. La forma recomendada de trabajar es usar bibliotecas externas. Para obtener ayuda para la creación de una biblioteca externa a partir del archivo jar, vea [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)

    Si no usa bibliotecas externas, debe proporcionar permisos a SQL Server para ejecutar las clases de Java en el archivo jar.

    Para conceder acceso de lectura y ejecución a un archivo jar, ejecute el siguiente comando **chmod** en el archivo jar. Se recomienda colocar siempre los archivos de clase en un archivo jar al trabajar con SQL Server. Para obtener ayuda para la creación de un archivo jar, vea [Cómo crear un archivo jar](https://docs.microsoft.com/sql/language-extensions/how-to/create-a-java-jar-file-from-class-files).

    ```cmd
    chmod ug+rx <MyJarFile.jar>
    ```

    También debe proporcionar permisos a mssql_satellite para leer o ejecutar el archivo jar.

    ```cmd
    chown mssql_satellite:mssql_satellite <MyJarFile.jar>
    ```

    La configuración adicional se realiza principalmente a través de la [herramienta mssql-conf](sql-server-linux-configure-mssql-conf.md).

2. Agregue la cuenta de usuario de mssql usada para ejecutar el servicio SQL Server. Esto es necesario si no ha ejecutado la instalación previamente.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

3. Habilite el acceso de red saliente. El acceso de red saliente está deshabilitado de forma predeterminada. Para habilitar las solicitudes salientes, establezca la propiedad booleana "outboundnetworkaccess" con la herramienta mssql-conf. Para obtener más información, vea [Configuración de SQL Server en Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md#mlservices-outbound-access).

   ```bash
   # Run as SUDO or root
   # Enable outbound requests over the network
   sudo /opt/mssql/bin/mssql-conf set extensibility outboundnetworkaccess 1
   ```

4. Reinicie el servicio SQL Server Launchpad y la instancia del motor de base de datos para leer los valores actualizados del archivo INI. En un mensaje de reinicio se le recuerda si se ha modificado un valor relacionado con la extensibilidad.  

   ```bash
   systemctl restart mssql-launchpadd

   systemctl restart mssql-server.service
   ```

5. Habilite la ejecución de scripts externos con Azure Data Studio u otra herramienta como SQL Server Management Studio (solo Windows) que ejecute Transact-SQL.

   ```bash
   EXEC sp_configure 'external scripts enabled', 1
   RECONFIGURE WITH OVERRIDE
   ```

6. Vuelva a reiniciar el servicio `mssql-launchpadd`.

7. Por cada base de datos en la que quiera usar Extensiones de lenguaje, debe registrar el lenguaje externo con [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql).

## <a name="register-external-language"></a>Registrar lenguaje externo

Por cada base de datos en la que quiera usar Extensiones de lenguaje, debe registrar el lenguaje externo con [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql).

En el ejemplo siguiente se agrega un lenguaje externo denominada Java a una base de datos en SQL Server en Linux.

```SQL
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'<path-to-tar.gz>', FILE_NAME = 'javaextension.so');
GO
```

Para obtener más información, vea [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql).

## <a name="verify-installation"></a>Comprobar la instalación

La integración de características de Java no incluye bibliotecas, pero puede ejecutar `grep -r JRE_HOME /etc` para confirmar la creación de la variable de entorno JAVA_HOME.

Para validar la instalación, ejecute un script de T-SQL que ejecute un procedimiento almacenado del sistema que invoque a Java. Necesita una herramienta de consulta para esta tarea. Azure Data Studio es una buena elección. Otras herramientas que se usan con frecuencia, como SQL Server Management Studio o PowerShell, son solo para Windows. Si tiene un equipo Windows con estas herramientas, úselo para conectarse a la instalación de Linux del motor de base de datos.

<a name="install-all"></a>

## <a name="full-install-of-sql-server-and-language-extensions"></a>Instalación completa de SQL Server y Extensiones de lenguaje

Puede instalar y configurar el motor de base de datos y Extensiones de lenguaje en un procedimiento si anexa paquetes y parámetros de Java a un comando que instala el motor de base de datos.

1. Proporcione una línea de comandos que incluya el motor de base de datos, además de las características de la extensión de lenguaje.

  Puede agregar extensibilidad de Java a la instalación de un motor de base de datos.

  ```bash
  sudo yum install -y mssql-server mssql-server-extensibility-java 
  ```

3. Acepte los contratos de licencia y complete la configuración posterior a la instalación. Use la herramienta **mssql-conf** para esta tarea.

  ```bash
  sudo /opt/mssql/bin/mssql-conf setup
  ```

  Se le pide que acepte el contrato de licencia del motor de base de datos, elija una edición y establezca la contraseña de administrador. 

4. Reinicie el servicio si se le pide.

  ```bash
  sudo systemctl restart mssql-server.service
  ```

## <a name="unattended-installation"></a>Instalación desatendida

Mediante la [instalación desatendida](https://docs.microsoft.com/sql/linux/sql-server-linux-setup#unattended) del motor de base de datos, agregue los paquetes de mssql-server-extensibility-java.

<a name="offline-install"></a>


## <a name="offline-installation"></a>Instalación sin conexión

Siga las instrucciones de [instalación sin conexión](sql-server-linux-setup.md#offline) para ver los pasos para instalar los paquetes. Busque el sitio de descarga y luego descargue paquetes específicos mediante la lista de paquetes siguiente.

> [!Tip]
> Varias de las herramientas de administración de paquetes proporcionan comandos que pueden ayudar a determinar las dependencias de los paquetes. En yum, use `sudo yum deplist [package]`. En Ubuntu, use `sudo apt-get install --reinstall --download-only [package name]` seguido de `dpkg -I [package name].deb`.

#### <a name="download-site"></a>Sitio de descarga

Puede descargar paquetes desde [https://packages.microsoft.com/](https://packages.microsoft.com/). Todos los paquetes de Java se colocan con el paquete del motor de base de datos. 

#### <a name="redhat7-paths"></a>Rutas de acceso de RedHat/7

|||
|--|----|
| Paquetes de mssql/extensibility-java | [https://packages.microsoft.com/rhel/7/mssql-server-preview/](https://packages.microsoft.com/rhel/7/mssql-server-preview/) |

#### <a name="ubuntu1604-paths"></a>Rutas de acceso de Ubuntu/16.04

|||
|--|----|
| Paquetes de mssql/extensibility-java | [https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/) |

#### <a name="suse12-paths"></a>Rutas de acceso de SUSE/12

|||
|--|----|
| Paquetes de mssql/extensibility-java | [https://packages.microsoft.com/sles/12/mssql-server-preview/](https://packages.microsoft.com/sles/12/mssql-server-preview/) |

#### <a name="package-list"></a>Lista de paquetes

En función de las extensiones que quiera usar, descargue los paquetes necesarios para un lenguaje específico. Los nombres de archivo exactos incluyen información de la plataforma en el sufijo, pero los nombres de archivo siguientes deben ser lo suficientemente cercanos para que pueda determinar qué archivos va a obtener.

```
# Core packages 
mssql-server-15.0.1000
mssql-server-extensibility-15.0.1000

# Java
mssql-server-extensibility-java-15.0.1000
```

## <a name="limitations-in-ctp-releases"></a>Limitaciones de las versiones CTP

Extensiones de lenguaje y la extensibilidad de Java en Linux todavía están en desarrollo activo. Las siguientes características aún no están habilitadas en la versión preliminar.

+ En este momento, la autenticación implícita no está disponible en Linux, lo que significa que no se puede volver a conectar al servidor desde Java en curso para acceder a datos u otros recursos.


### <a name="resource-governance"></a>Regulación de recursos

Existe paridad entre Linux y Windows para la [regulación de recursos](../t-sql/statements/create-external-resource-pool-transact-sql.md) de los grupos de recursos externos, pero las estadísticas de [sys.dm_resource_governor_external_resource_pools](../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pools.md) tienen actualmente unidades diferentes en Linux. Las unidades se van a alinear en una próxima versión CTP.
 
| Nombre de columna   | Descripción | Valor en Linux | 
|---------------|--------------|---------------|
|peak_memory_kb | Cantidad máxima de memoria usada para el grupo de recursos. | En Linux, esta estadística tiene como origen el subsistema CGroups memory, donde el valor es memory.max_usage_in_bytes |
|write_io_count | Total de operaciones de E/S de escritura emitidas desde el restablecimiento de las estadísticas de Resource Governor. | En Linux, esta estadística tiene como origen el subsistema CGroups blkio, donde el valor de la fila de escritura es blkio.throttle.io_serviced | 
|read_io_count | Total de operaciones de E/S de lectura emitidas desde el restablecimiento de las estadísticas de Resource Governor. | En Linux, esta estadística tiene como origen el subsistema CGroups blkio, donde el valor de la fila de lectura es blkio.throttle.io_serviced | 
|total_cpu_kernel_ms | Tiempo del kernel de usuario de CPU acumulativo en milisegundos desde el restablecimiento de las estadísticas de Resource Governor. | En Linux, esta estadística tiene como origen el subsistema CGroups cpuacct, donde el valor de la fila de usuario es cpuacct.stat |  
|total_cpu_user_ms | Tiempo de usuario de CPU acumulativo en milisegundos desde el restablecimiento de las estadísticas de Resource Governor.| En Linux, esta estadística tiene como origen el subsistema CGroups cpuacct, donde el valor de la fila de sistema es cpuacct.stat | 
|active_processes_count | Número de procesos externos que se ejecutan en el momento de la solicitud.| En Linux, esta estadística tiene como origen el subsistema GGroups pids, donde el valor es pids.current | 

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de Java pueden empezar con algunos ejemplos sencillos y conocer los aspectos básicos del funcionamiento de Java con SQL Server. Para el siguiente paso, vea los vínculos siguientes:

+ [Tutorial: Expresiones regulares con Java](../language-extensions/tutorials/search-for-string-using-regular-expressions-in-java.md)