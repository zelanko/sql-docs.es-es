---
title: Instalación de un entorno de ejecución personalizado de Python
description: Obtenga información sobre cómo instalar un entorno de ejecución personalizado de Python para SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/20/2020
ms.topic: how-to
author: cawrites
ms.author: chadam
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d02217eaae3cf402a1ccb6e08780f4e9406d446f
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956397"
---
# <a name="install-a-python-custom-runtime-for-sql-server"></a>Instalación de un entorno de ejecución personalizado de Python para SQL Server
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

En este artículo se describe cómo instalar un entorno de ejecución personalizado para ejecutar scripts de Python con SQL Server. El tiempo de ejecución personalizado usa la tecnología de extensión de lenguaje basada en un marco de extensibilidad para ejecutar código externo. El entorno de ejecución personalizado para Python se puede usar en los escenarios siguientes:

+ Una instalación de SQL Server con el marco de extensibilidad.

+ Una instalación de Machine Learning Services con SQL Server 2019. La extensión de lenguaje se puede usar con [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) después de completar algunos pasos de configuración adicionales.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

> [!NOTE]
> En este artículo se describe cómo instalar un entorno de ejecución personalizado para Python en Windows. Para instalar en Linux, consulte [Instalación de un entorno de ejecución personalizado de Python para SQL Server en Linux](custom-runtime-python.md?view=sql-server-linux-ver15&preserve-view=true).



## <a name="pre-install-checklist"></a>Lista de comprobación previa a la instalación

Antes de instalar un entorno de ejecución personalizado de Python, instale lo siguiente:

+ [SQL Server 2019 para Windows CU3 o posterior](../../database-engine/install-windows/install-sql-server.md).

  > [!NOTE]
  > El entorno de ejecución personalizado de Python requiere la actualización acumulativa (CU) 3 o posterior para SQL Server 2019.

+ [Extensiones de lenguaje de SQL Server en Windows con el marco de extensibilidad](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md).

+ [Python 3.7]( https://www.python.org/downloads/release/python-379/).

## <a name="add-sql-server-language-extensions-for-windows"></a>Adición de las extensiones de lenguaje de SQL Server para Windows

> [!NOTE]
> Si ha instalado Machine Learning Services en SQL Server 2019, el marco de extensibilidad ya está instalado y puede omitir este paso.

Las extensiones de lenguaje usan el marco de extensibilidad para ejecutar código externo. La ejecución del código está aislada de los procesos principales del motor, pero está totalmente integrada con la ejecución de consultas de SQL Server.

1. Inicie el asistente para la instalación de SQL Server 2019.
  
1. En la pestaña **Instalación**, seleccione **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.
    
    ![Instalación de SQL Server 2019 CU3 o posterior](../install/media/2019setup-installation-page-mlsvcs.png) 

1. En la página **Selección de características** , seleccione estas opciones:
  
    - **Servicios de Motor de base de datos**
  
        Para usar las extensiones de lenguaje con SQL Server, debe instalar una instancia del motor de base de datos. Puede usar una instancia predeterminada o una con nombre.
  
    - **Machine Learning Services y extensiones de lenguaje**
   
       Seleccione **Machine Learning Services y extensiones de lenguaje**. No es necesario seleccionar Python.

    ![Características de la instalación de SQL Server 2019 CU3 o posterior](../install/media/sql-feature-selection.png) 

1. En la página **Listo para instalar**, confirme que estas selecciones se han realizado y haga clic en **Instalar**.
  
    + Servicios de Motor de base de datos
    + Machine Learning Services y extensiones de lenguaje

1. Cuando finalice la instalación, si el programa indica que se reinicie el equipo, hágalo. Es importante leer el mensaje del Asistente para la instalación tras finalizar el programa de instalación. Para obtener más información, vea [View and Read SQL Server Setup Log Files](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).


## <a name="install-python-37"></a>Instalación de Python 3.7 

Instale [Python 3.7]( https://www.python.org/downloads/release/python-379/) y agréguelo a la ruta de acceso.

![Agregar Python 3.7 a la ruta de acceso.](../install/media/python-379.png) 


#### <a name="install-pandas"></a>Instalación de pandas

Instale el paquete para Python [pandas](https://pandas.pydata.org/) desde un símbolo del sistema con privilegios *elevados*:

```bash
python.exe -m pip install pandas
```

## <a name="update-the-system-environment-variables"></a>Actualización de las variables de entorno del sistema

Agregue o modifique PYTHONHOME como variable de entorno del sistema.

+ En el cuadro de búsqueda de Windows, escriba "entorno" y seleccione **Editar las variables de entorno del sistema**.
+ En la pestaña **Opciones avanzadas**, seleccione **Variables de entorno**.
+ En **Variables del sistema**, seleccione **Nueva** para crear PYTHONHOME para que apunte a la ubicación de instalación de Python 3.7.
Si PYTHONHOME ya existe, seleccione **Editar** para que apunte a la ubicación de instalación de Python 3.7.
+ Seleccione **Aceptar** para cerrar las ventanas restantes.

![Cree la variable del sistema PYTHONHOME.](../install/media/sys-pythonhome.png)

## <a name="grant-access-to-the-custom-python-installation-folder"></a>Concesión de acceso a la carpeta de instalación personalizada de Python

Ejecute los siguientes comandos **icacls** desde un nuevo símbolo del sistema con privilegios *elevados* para conceder acceso de lectura y ejecución al **servicio SQL Server Launchpad** y SID **S-1-15-2-1** (**ALL_APPLICATION_PACKAGES**). El nombre de usuario del servicio Launchpad (`NT Service\MSSQLLAUNCHPAD$INSTANCENAME* where INSTANCENAME`) es el nombre de la instancia de SQL Server. Estos comandos concederán acceso de forma recursiva a todos los archivos y carpetas en la ruta de acceso de directorio especificada.

Anexe el nombre de la instancia a `MSSQLLAUNCHPAD` (`MSSQLLAUNCHPAD$INSTANCENAME`). En este ejemplo, INSTANCENAME es la instancia predeterminada `MSSQLSERVER`.

1. Conceda permisos al **nombre de usuario del servicio SQL Server Launchpad**.

    ```cmd
    icacls "%PYTHONHOME%" /grant "NT Service\MSSQLLAUNCHPAD$MSSQLSERVER":(OI)(CI)RX /T

2. Give permissions to **SID S-1-15-2-1**.
    ```cmd
    icacls "%PYTHONHOME%" /grant *S-1-15-2-1:(OI)(CI)RX /T

>[!NOTE]
>The preceding command grants permissions to the computer **SID S-1-15-2-1**, which is equivalent to ALL APPLICATION PACKAGES on an English version of Windows. Alternatively, you can use `icacls "%R_HOME%" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` on an English version of Windows.

## Restart SQL Server Launchpad service

From an *elevated* command prompt, run the following commands. Replace "MSSQLSERVER" with the name of your SQL Server instance.

```CMD
net stop MSSQLLAUNCHPAD$MSSQLSERVER
net start MSSQLLAUNCHPAD$MSSQLSERVER
```

Como alternativa, haga clic con el botón derecho en el servicio SQL Server Launchpad en la aplicación **Servicios** del sistema y haga clic en el comando **Reiniciar**. O bien, utilice el [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md) para reiniciar el servicio.

## <a name="download-python-language-extension"></a>Descarga de la extensión del lenguaje Python

Descargue el [archivo ZIP que contiene la extensión del lenguaje Python para Windows](https://github.com/microsoft/sql-server-language-extensions/releases). Se recomienda usar la versión de lanzamiento en producción. Use la versión de depuración en desarrollo o pruebas, ya que proporciona información de registro detallada para investigar los errores.

## <a name="register-external-language"></a>Registrar lenguaje externo

Registre esta extensión del lenguaje Python con [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) para cada base de datos en la que desea usarla. Use [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) para conectarse a SQL Server y ejecute el siguiente comando T-SQL. Modifique la ruta de acceso de esta instrucción para reflejar la ubicación del archivo ZIP de la extensión de lenguaje descargado (python-lang-extension.zip).

> [!NOTE]
> Python es una palabra reservada. Use un nombre diferente para el lenguaje externo, por ejemplo, "myPython".

```sql
CREATE EXTERNAL LANGUAGE [myPython]
FROM (CONTENT = N'/path/to/python-lang-extension.zip', FILE_NAME = 'pythonextension.dll');
GO
```

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

Puede instalar SQL Server en Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) y Ubuntu. Para obtener más información, vea [la sección Plataformas admitidas de las instrucciones de instalación de SQL Server en Linux](../../linux/sql-server-linux-setup.md).

> [!NOTE]
> En este artículo se describe cómo instalar un entorno de ejecución personalizado para Python en Linux. Para instalar en Windows, consulte [Instalación de un entorno de ejecución personalizado de Python para SQL Server en Windows](custom-runtime-python.md?view=sql-server-ver15&preserve-view=true).

## <a name="pre-install-checklist"></a>Lista de comprobación previa a la instalación

Antes de instalar un entorno de ejecución personalizado de Python, instale lo siguiente:

+ [SQL Server 2019 para Linux (actualización acumulativa 3 o posterior)](../../linux/sql-server-linux-setup.md).
Al instalar SQL Server en Linux, debe configurar un repositorio de Microsoft. Para más información, consulte [Configuración de repositorios](../../linux/sql-server-linux-change-repo.md).

  > [!NOTE]
  > El entorno de ejecución personalizado de Python requiere la actualización acumulativa (CU) 3 o posterior para SQL Server 2019.

+ [Extensiones de lenguaje de SQL Server en Linux con el marco de extensibilidad](../../linux/sql-server-linux-setup-language-extensions.md).

+ [Python 3.7](https://www.python.org/downloads/release/python-379/).

## <a name="add-sql-server-language-extensions-for-linux"></a>Adición de las extensiones de lenguaje de SQL Server para Linux

> [!NOTE]
> Si ha instalado Machine Learning Services en SQL Server 2019, el paquete **mssql-server-extensibility** para las extensiones de lenguaje ya está instalado y puede omitir este paso.

Las extensiones de lenguaje usan el marco de extensibilidad para ejecutar código externo. La ejecución del código está aislada de los procesos principales del motor, pero está totalmente integrada con la ejecución de consultas de SQL Server.

Use los siguientes comandos para instalar las extensiones de lenguaje, en función de la versión de Linux.

### <a name="ubuntu"></a>Ubuntu
> [!TIP]
> Si es posible, ejecute `update` para actualizar los paquetes en el sistema antes de la instalación. Ubuntu podría no tener la opción de transporte de apt para https. Para instalarla, use `apt-get install apt-transport-https`.

```bash
# Install as root or sudo
sudo apt-get install mssql-server-extensibility
```

### <a name="red-hat"></a>Red Hat
```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility
```

### <a name="suse"></a>Suse
```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility
```

## <a name="install-python-37-and-pandas"></a>Instalación de Python 3.7 y pandas

Instale Python 3.7, la biblioteca libpython3.7 y el paquete pandas. 

Los siguientes son comandos de ejemplo para Ubuntu:

```bash
# Install python3.7 and the corresponding library:
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.7 python3-pip libpython3.7

# Install pandas to /usr/lib:
sudo python3.7 -m pip install pandas -t /usr/lib/python3.7/dist-packages
```

## <a name="using-a-custom-installation-of-python-37"></a>Uso de una instalación personalizada de Python 3.7

> [!NOTE]
> Si ha instalado Python en la ubicación predeterminada `/usr/lib/python3.7`, puede ir directamente a [la sección siguiente](#download-python-linux).

Si ha compilado su propia versión de Python 3.7, use los siguientes comandos para que SQL Server pueda encontrar y cargar la instalación personalizada.

### <a name="update-the-environment-variables"></a>Actualización de las variables de entorno

1. Edite el servicio Microsoft mssql-launchpadd para agregar la variable de entorno PYTHONHOME al archivo `/etc/systemd/system/mssql-launchpadd.service.d/override.conf`.

      ```bash
      sudo systemctl edit mssql-launchpadd
      ```

    + Inserte el texto siguiente en el archivo `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` que se abre. Establezca el valor de PYTHONHOME en la ruta de instalación personalizada de Python.

      ```vi
      [Service]
      Environment="PYTHONHOME=/path/to/installation/of/python3.7"
      ```

    + Guarde y cierre el archivo.

2. Asegúrese de que se puede cargar `libpython3.7m.so.1.0`.

    + Cree el archivo custom-python.conf en `/etc/ld.so.conf.d`.

      ```bash
      sudo vi /etc/ld.so.conf.d/custom-python.conf
      ```

    + En el archivo que se abre, agregue la ruta de acceso a **libpython3.7m.so.1.0** de la instalación personalizada de Python.

      ```vi
      /path/to/installation/of/python3.7/lib
      ```

    + Guarde y cierre el nuevo archivo.

    + Ejecute `ldconfig` y compruebe que se puede cargar `libpython3.7m.so.1.0`; para ello, ejecute los comandos siguientes y compruebe que se pueden encontrar todas las bibliotecas dependientes.

      ```bash
      sudo ldconfig
      ldd /path/to/installation/of/python3.7/lib/libpython3.7m.so.1.0
      ```

### <a name="grant-access-to-the-custom-python-folder"></a>Concesión de acceso a la carpeta de instalación personalizada de Python

Establezca la opción `datadirectories` de la sección de extensibilidad del archivo /var/opt/mssql/mssql.conf en la instalación personalizada de Python.

```bash
sudo /opt/mssql/bin/mssql-conf set extensibility.datadirectories /path/to/installation/of/python3.7
```

### <a name="restart-the-mssql-launchpadd-service"></a>Reinicio del servicio mssql-launchpadd

```bash
sudo systemctl restart mssql-launchpadd
```
## <a name="download-python-language-extension"></a><a name="download-python-linux"></a>Descarga de la extensión del lenguaje Python

Descargue el [archivo ZIP que contiene la extensión del lenguaje Python para Linux](https://github.com/microsoft/sql-server-language-extensions/releases). Se recomienda usar la versión de lanzamiento en producción. Use la versión de depuración en desarrollo o pruebas, ya que proporciona información de registro detallada para investigar los errores.

## <a name="register-external-language"></a>Registrar lenguaje externo

Registre esta extensión del lenguaje Python con [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) para cada base de datos en la que desea usarla. Use [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md) para conectarse a SQL Server y ejecute el siguiente comando T-SQL. 
Modifique la ruta de acceso de esta instrucción para reflejar la ubicación del archivo ZIP de la extensión de lenguaje descargado (python-lang-extension.zip).

> [!NOTE]
>Python es una palabra reservada. Use un nombre diferente para el lenguaje externo, por ejemplo, "myPython".

```sql
CREATE EXTERNAL LANGUAGE myPython 
FROM (CONTENT = N'/PATH/TO/python-lang-extension.zip', FILE_NAME = 'libPythonExtension.so.1.0');
GO
```

::: moniker-end

## <a name="enable-external-script-execution-in-sql-server"></a>Habilitación de la ejecución de scripts externos en SQL Server

Se puede ejecutar un script externo en Python mediante la ejecución del procedimiento almacenado [sp_execute_external script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) en SQL Server. 

Para habilitar los scripts externos, ejecute los siguientes comandos SQL con [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md), conectado a SQL Server.

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

## <a name="verify-language-extension-installation"></a>Comprobación de la instalación de la extensión de lenguaje

Este script de SQL prueba la funcionalidad de la extensión de lenguaje instalada.

```sql
EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
import sys
print(sys.path)
print(sys.version)
print(sys.executable)'
```

## <a name="verify-parameters-and-datasets-of-different-data-types"></a>Comprobación de los parámetros y los conjuntos de datos de diferentes tipos de datos

Este script prueba diferentes tipos de datos para los parámetros de entrada y salida y los conjuntos de datos.

```sql
DECLARE @sumVal int = 12;
DECLARE @charVal VARCHAR(30) = N'Hello'

EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
print(sumVal)
print(charVal)
sumVal = sumVal + 300
OutputDataSet = InputDataSet'
,@input_data_1 = N'SELECT 1, CAST(1.4 as real), ''Hi'', CAST(''1'' as bit)'
,@params = N'@sumVal int OUTPUT, @charVal VARCHAR(30)'
,@sumVal = @sumVal OUTPUT
,@charVal = @charVal
WITH RESULT SETS ((intCol int, doubleCol real, charCol char(2), logicalCol bit));

PRINT @sumVal
```

## <a name="next-steps"></a>Pasos siguientes

+ [Marco de extensibilidad en SQL Server](../concepts/extensibility-framework.md)
+ [Introducción a las extensiones de lenguaje](../../language-extensions/language-extensions-overview.md)