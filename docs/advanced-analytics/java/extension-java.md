---
title: 'Extensión del lenguaje Java en SQL Server 2019: SQL Server Machine Learning Services'
description: Instalar, configurar y validar la extensión del lenguaje Java en SQL Server 2019 para los sistemas Linux y Windows.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/07/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a258573ff7506f2533c2f91edb5751cfd1121dc8
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431719"
---
# <a name="java-language-extension-in-sql-server-2019"></a>Extensión del lenguaje Java en SQL Server 2019 

A partir de SQL Server 2019 preview en Windows y Linux, puede ejecutar código de Java personalizado en el [marco de extensibilidad](../concepts/extensibility-framework.md) como complemento a la instancia del motor de base de datos. 

El marco de extensibilidad es una arquitectura para la ejecución de código externo: Java (a partir de SQL Server 2019), [Python (a partir de SQL Server 2017)](../concepts/extension-python.md), y [R (a partir de SQL Server 2016)](../concepts/extension-r.md). Ejecución de código está aislada de los procesos del motor principal, pero totalmente integrada con la ejecución de consultas de SQL Server. Esto significa que puede insertar los datos de cualquier consulta de SQL Server para el tiempo de ejecución externo y consumir o conservar los resultados de vuelta en SQL Server.

Al igual que con cualquier extensión del lenguaje de programación, el procedimiento almacenado del sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) es la interfaz para ejecutar código de Java compilado previamente.

## <a name="prerequisites"></a>Requisitos previos

Se requiere una instancia de la versión preliminar de SQL Server 2019. Las versiones anteriores no tienen integración con Java. 

Requisitos de la versión de Java varían entre Windows y Linux. El requisito mínimo es de Java Runtime Environment (JRE), pero es útil si necesita el compilador de Java o los paquetes de desarrollo JDK. Dado el JDK es totalmente inclusivo, si instala el JDK y JRE no es necesario.

| Sistema operativo | Versión de Java | Descarga JRE | Descarga de JDK |
|------------------|--------------|--------------|--------------|
| Windows          | 1.10         | [JRE 10](https://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html) | [JDK 10](https://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html)  |
| Linux            | 1.8          |  [JRE 8](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) | [JDK 8](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)  |  

En Linux, el **mssql-server-extensibilidad-java** paquete instala automáticamente JRE 1.8 si ya no está instalado. Scripts de instalación también agregar la ruta de acceso JVM a una variable de entorno llamada JAVA_HOME.

En Windows, se recomienda instalar el JDK en el valor predeterminado /Program archivos / carpetas si es posible. En caso contrario, se requiere configuración adicional para conceder permisos a los archivos ejecutables. Para obtener más información, consulte el [conceder permisos (Windows)](#perms-nonwindows) sección en este documento.

> [!Note]
> Dado que Java es compatible con versiones anteriores, las versiones anteriores podrían funcionar, pero las versiones admitidas y probadas para esta versión CTP anterior se muestran en la tabla.

<a name="install-on-linux"></a>

## <a name="install-on-linux"></a>Instalación en Linux

Puede instalar el [bases de datos motor y la extensión de Java juntos](../../linux/sql-server-linux-setup-machine-learning.md#install-all), o agregar compatibilidad con Java en una instancia existente. Los ejemplos siguientes agregue la extensión de Java a una instalación existente.  

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility-java

# USE install commands
sudo zypper install mssql-server-extensibility-java
```

Al instalar **mssql-server-extensibilidad-java**, el paquete instala automáticamente JRE 1.8 si ya no está instalado. También agregará la ruta de acceso JVM para una variable de entorno llamada JAVA_HOME.

Después de completar la instalación, el siguiente paso es [configurar ejecución de scripts externos](#configure-script-execution).

> [!Note]
> En un dispositivo conectado a internet, las dependencias del paquete se descargó e instaló como parte de la instalación del paquete principal. Para obtener más detalles, el programa de instalación sin conexión, consulte [instalar SQL Server Machine Learning en Linux](../../linux/sql-server-linux-setup-machine-learning.md).

### <a name="grant-permissions-on-linux"></a>Conceder permisos en Linux

Para proporcionar permisos para ejecutar las clases de Java a SQL Server, deberá establecer los permisos.

Para conceder acceso y ejecución para jar de archivos o archivos de clase, ejecute el siguiente **chmod** comando en cada archivo de clase o el archivo jar. Se recomienda colocar los archivos de clase en un archivo jar cuando se trabaja con SQL Server. Para obtener ayuda acerca de la creación de un archivo jar, consulte [cómo crear un archivo jar](#create-jar).

```cmd
chmod ug+rx <MyJarFile.jar>
```
También deberá conceder permisos de mssql_satellite en el archivo del directorio o archivo jar para lectura y ejecución.

* Si se llama a archivos de clase de SQL Server, mssql_satellite necesita leer/ejecutará los permisos en *cada* directorio en la jerarquía de carpetas, desde la raíz hasta el elemento primario directo.

* Si se llama a un archivo jar desde SQL Server, es suficiente para ejecutar el comando en el propio archivo jar.

```cmd
chown mssql_satellite:mssql_satellite <directory>
```

```cmd
chown mssql_satellite:mssql_satellite <MyJarFile.jar>
```

<a name="install-on-windows"></a>

## <a name="install-on-windows"></a>Instalar en Windows

1. [Ejecute el programa de instalación](../install/sql-machine-learning-services-windows-install.md) para instalar SQL Server 2019.

2. Cuando llegue a la selección de características, elija **Machine Learning Services (en bases de datos)**. 

   Aunque la integración de Java no se incluye con bibliotecas de aprendizaje automático, esta es la opción de instalación que proporciona el marco de extensibilidad. Si lo desea puede omitir R y Python.

3. Finalizar al Asistente para instalación y, a continuación, continúe con las siguientes dos tareas.

### <a name="add-the-javahome-variable"></a>Agregue la variable JAVA_HOME

JAVA_HOME es una variable de entorno que especifica la ubicación del intérprete de Java. En este paso, creará una variable de entorno del sistema para él en Windows.

1. Busque y copie la ruta de instalación de JDK y JRE (por ejemplo, C:\Program Files\Java\jdk-10.0.2).

  En CTP 2.0, si se establece JAVA_HOME en la carpeta base jdk solo funciona para Java 1.10. 

  Para Java 1.8, extender la ruta de acceso para llegar a la jvm.dll en Windows en su JDK (por ejemplo, "C:\Program Files\Java\jdk1.8.0_181\bin\server". Como alternativa, puede apuntar a una carpeta de base de JRE: "C:\Program Files\Java\jre1.8.0_181".

2. En el Panel de Control, abra **sistema y seguridad**, abra **sistema**y haga clic en **propiedades avanzadas de sistema**.

3. Haga clic en **Variables de entorno**.

4. Cree una nueva variable del sistema para JAVA_HOME.

   ![Variable de entorno para el hogar Java](../media/java/env-variable-java-home.png "de instalación de Java")

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jdk-folder-windows-only"></a>Conceder acceso a la carpeta JDK no predeterminada (solo Windows)

Puede omitir este paso si ha instalado el JDK y JRE en la carpeta predeterminada. 

Una instalación de la carpeta no predeterminada, ejecute el **icacls** comandos desde un *con privilegios elevados* línea para conceder acceso a la **SQLRUsergroup** y cuentas de servicio de SQL Server (en  **ALL_APPLICATION_PACKAGES**) para acceder a la JVM y el classpath de Java. Los comandos realizará de forma recursiva conceder acceso a todos los archivos y carpetas bajo la ruta de acceso del directorio dado.

#### <a name="sqlrusergroup-permissions"></a>SQLRUserGroup permisos

Para una instancia con nombre, anexe el nombre de instancia al SQLRUsergroup (por ejemplo, `SQLRUsergroupINSTANCENAME`).

```cmd
icacls "<PATH TO CLASS or JAR FILES>" /grant "SQLRUsergroup":(OI)(CI)RX /T
```

#### <a name="appcontainer-permissions"></a>Permisos de AppContainer

```cmd
icacls "PATH to JDK/JRE" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T
```

### <a name="add-the-jre-path-to-javahome"></a>Agregue la ruta JRE JAVA_HOME
También deberá agregar la ruta de acceso a JRE en la variable de entorno JAVA_HOME. Si solo tiene un JRE instalado, puede proporcionar la ruta de acceso de carpeta JRE. Sin embargo, si tiene un JDK instalado, deberá proporcionar la ruta de acceso completa a la JVM, en la carpeta JRE en JDK, similar al siguiente: "C:\Program Files\Java\jdk1.8.0_191\jre\bin\server".

Para crear una variable del sistema, use el Panel de Control > sistema y seguridad > sistema tenga acceso a **propiedades avanzadas de sistema**. Haga clic en **Variables de entorno** y, a continuación, cree una nueva variable del sistema para JAVA_HOME.

![Variable de entorno para el hogar Java](../media/java/env-variable-java-home.png "de instalación de Java")

<a name="configure-script-execution"></a>

## <a name="configure-script-execution"></a>Configurar la ejecución del script

En este momento, está casi listo para ejecutar código de Java en Linux o Windows. Como último paso, cambiar a SQL Server Management Studio u otra herramienta que se ejecuta el script de Transact-SQL para habilitar la ejecución de scripts externos.

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="verify-installation"></a>Comprobar la instalación

Para confirmar la instalación está operativa, crear y ejecutar un [aplicación de ejemplo](java-first-sample.md) utilizando el JDK que se ha instalado, la colocación de los archivos en la ruta de clase que configuró anteriormente.

## <a name="differences-in-ctp-20"></a>Diferencias en CTP 2.0

Si ya está familiarizado con Machine Learning Services, ha cambiado el modelo de autorización y aislamiento para las extensiones en esta versión. Para obtener más información, consulte [diferencias en una instalación de SQL Server Machine Learning de 2019 Services](../install/sql-machine-learning-services-ver15.md).

## <a name="limitations-in-ctp-20"></a>Limitaciones en CTP 2.0

* No puede superar el número de valores de los búferes de entrada y salidos `MAX_INT (2^31-1)` , ya que es el número máximo de elementos que se pueden asignar en una matriz en Java.

* Parámetros de salida [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) no se admiten en esta versión.

* Ningún tipo de datos LOB soporte técnico para los conjuntos de datos de entrada y salida en esta versión. Consulte [tipos de datos de SQL Server y Java](java-sql-datatypes.md) para obtener más información acerca de los datos que se admiten los tipos en esta versión de CTP.

* Streaming con el parámetro sp_execute_external_script @r_rowsPerRead no se admite en esta versión de CTP.

* Creación de particiones mediante el parámetro sp_execute_external_script @input_data_1_partition_by_columns no se admite en esta versión de CTP.

<a name="create-jar"></a>

## <a name="how-to-create-a-jar-file-from-class-files"></a>Cómo crear un archivo jar desde archivos de clase

Navegue hasta la carpeta que contiene el archivo de clase y ejecute este comando:

```cmd
jar -cf <MyJar.jar> *.class
```

Asegúrese de que la ruta de acceso **jar.exe** forma parte de la variable de ruta de acceso del sistema. Como alternativa, especifique la ruta de acceso completa al archivo jar que se encuentra en/bin en la carpeta JDK: `C:\Users\MyUser\Desktop\jdk-10.0.2\bin\jar -cf <MyJar.jar> *.class`

## <a name="next-steps"></a>Pasos siguientes

+ [Cómo llamar a Java en SQL Server](howto-call-java-from-sql.md)
+ [Ejemplo de Java en SQL Server](java-first-sample.md)
+ [Tipos de datos de SQL Server y Java](java-sql-datatypes.md)