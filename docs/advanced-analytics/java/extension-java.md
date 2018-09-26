---
title: Extensión del lenguaje Java en SQL Server 2019 | Microsoft Docs
description: Ejecutar código de Java en SQL Server 2019 mediante la extensión del lenguaje Java.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8acb0a72435306cdec8740ffb41ff499eea61fac
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715370"
---
# <a name="java-language-extension-in-sql-server-2019"></a>Extensión del lenguaje Java en SQL Server 2019 

A partir de SQL Server 2019, puede ejecutar código de Java personalizado en el [marco de extensibilidad](../concepts/extensibility-framework.md) como complemento a la instancia del motor de base de datos. 

El marco de extensibilidad es una arquitectura para la ejecución de código externo: Java (a partir de SQL Server 2019), [Python (a partir de SQL Server 2017)](../concepts/extension-python.md), y [R (a partir de SQL Server 2016)](../concepts/extension-r.md). Ejecución de código está aislada de los procesos del motor principal, pero totalmente integrada con la ejecución de consultas de SQL Server. Esto significa que puede insertar los datos de cualquier consulta de SQL Server para el tiempo de ejecución externo y consumir o conservar los resultados de vuelta en SQL Server.

Al igual que con cualquier extensión del lenguaje de programación, el procedimiento almacenado del sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) es la interfaz para ejecutar código de Java compilado previamente.

## <a name="1---feature-installation"></a>1 - instalación de características

Ejecute el programa de instalación de SQL Server de 2019 en Windows o Linux para instalar la extensión del lenguaje Java. Se requiere una instancia del motor de base de datos de SQL Server 2019. No se puede agregar la integración de Java a versiones anteriores.

En Windows, inicie el [Asistente para la instalación](../install/sql-machine-learning-services-windows-install.md). En selección de características, seleccione **Machine Learning Services (en bases de datos)**. Aunque la integración de Java no se incluye con bibliotecas de aprendizaje automático, esta es la opción de instalación que proporciona el marco de extensibilidad. Si lo desea puede omitir R y Python.

En Linux, instale el [motor de base de datos](https://docs.microsoft.com/sql/linux/sql-server-linux-setup), así como el [extensión, Java y extensibilidad paquete](../../linux/sql-server-linux-setup-machine-learning.md).

Los ejemplos siguientes ilustran la sintaxis para cada sistema operativo de Linux.

```bash
# RedHat install commands
sudo yum install mssql-server-extensibility
sudo yum install mssql-server-extensibility-java

# Ubuntu install commands
sudo apt-get install mssql-server-extensibility
sudo apt-get install mssql-server-extensibility-java

# USE install commands
sudo zypper install mssql-server-extensibility
sudo zypper install mssql-server-extensibility-java
```

## <a name="2---configuration"></a>2 - Configuración

Con SQL Server Management Studio u otra herramienta que se ejecuta el script de Transact-SQL, configure la ejecución del script externo en la instancia del motor de base de datos.

  ```sql
  EXEC sp_configure 'external scripts enabled', 1
  RECONFIGURE WITH OVERRIDE
-- No restart is required after this step as of SQl Server 2019
 ```

## <a name="3---bring-your-own-java"></a>3 - traiga su propia Java

Una diferencia del anterior integraciones de lenguaje como R y Python es que usted pueda controlar que JVM se utiliza con SQL Server.

| Versión de Java | Sistema operativo |
|--------------|------------------|
| [1.10 Java](http://jdk.java.net/10/)   | Windows |
| Java 1.8   | Linux | 

Dado que Java es compatible con versiones anteriores, las versiones anteriores podrían funcionar, pero las versiones admitidas y probadas para esta versión CTP anterior se muestran en la tabla.

> [!Note]
>Para ejecutar Java con SQL Server, técnicamente solo necesita el [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre10-downloads-4417026.html) instalado (JRE). El JDK es el desarrollo de paquetes relacionados con el kit como el compilador de Java y otros entornos de desarrollo. Si ya tiene un entorno de desarrollo y solo necesita un tiempo de ejecución de Java en el equipo del servidor, puede omitir las instrucciones de instalación de JDK y solo instalar JRE.

## <a name="jdk-on-windows"></a>JDK en Windows

Descargue la versión de Windows de la [Java SE Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk10-downloads-4416644.html).

Instalar el JDK en el valor predeterminado de archivos /Program / lectura de la carpeta si desea evitar tener que conceder permiso a **todos los paquetes de aplicación** y **SQLRUserGroup** grupos de seguridad en una ubicación alternativa . Se aplica la misma guía para el acceso a sus carpetas de classpath de Java, donde guarda los archivos .class o. jar. 

> [!Note]
> Ha cambiado el modelo de autorización y aislamiento para las extensiones en esta versión. Para obtener más información, consulte [diferencias en una instalación de SQL Server Machine Learning de 2019 Services](../install/sql-machine-learning-services-ver15.md).

<a name="perms-nonwindows"></a>

### <a name="grant-access-to-non-default-jdk-folder-windows-only"></a>Conceder acceso a la carpeta JDK no predeterminada (solo Windows)

Puede omitir este paso si ha instalado el JDK y JRE en la carpeta predeterminada. Para una instalación de la carpeta no predeterminada, ejecute los siguientes scripts de PowerShell para conceder acceso a la **SQLRUsergroup** y cuentas de servicio de SQL Server (en ALL_APPLICATION_PACKAGES) para acceder a la JVM y el classpath de Java.

#### <a name="sqlrusergroup-permissions"></a>SQLRUserGroup permisos

```powershell
$Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>"
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("SQLRUsergroup","FullControl","Allow")
$Acl.SetAccessRule($Ar)
Set-Acl ""<YOUR PATH TO JDK / CLASSPATH>" $Acl 
```

#### <a name="appcontainer-permissions"></a>Permisos de AppContainer

```powershell
$Acl = Get-Acl "<YOUR PATH TO JDK / CLASSPATH>" 
$Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("ALL APPLICATION PACKAGES","FullControl","Allow") 
$Acl.SetAccessRule($Ar) 
Set-Acl "<YOUR PATH TO JDK / CLASSPATH>" $Acl 
```

### <a name="add-the-jdk-path-to-javahome"></a>Agregue la ruta JDK JAVA_HOME
También deberá agregar la ruta de instalación de JDK y JRE (por ejemplo, "C:\Program Files\Java\jdk-10.0.2") a una variable de entorno del sistema que se denomine "JAVA_HOME". 

Para crear una variable del sistema, use el Panel de Control > sistema y seguridad > sistema tenga acceso a **propiedades avanzadas de sistema**. Haga clic en **Variables de entorno** y, a continuación, cree una nueva variable del sistema para JAVA_HOME.

![Variable de entorno para el hogar Java](../media/java/env-variable-java-home.png "de instalación de Java")

## <a name="jdk-on-linux"></a>JDK en Linux

En Linux, el paquete mssql-server-extensibilidad-java instala automáticamente JRE 1.8 si ya no está instalado. También agregará la ruta de acceso JVM para una variable de entorno llamada JAVA_HOME.

## <a name="limitations-in-ctp-20"></a>Limitaciones en CTP 2.0

* No puede superar el número de valores de los búferes de entrada y salidos `MAX_INT (2^31-1)` , ya que es el número máximo de elementos que se pueden asignar en una matriz en Java.

* Los parámetros de salida en sp_execute_external_script no se admiten en esta versión.

* Ningún tipo de datos LOB soporte técnico para los conjuntos de datos de entrada y salida en esta versión. Consulte [tipos de datos de SQL Server y Java](java-sql-datatypes.md) para obtener más información acerca de los datos que se admiten los tipos en esta versión de CTP.

* Streaming con el parámetro sp_execute_external_script @r_rowsPerRead no se admite en esta versión de CTP.

* Creación de particiones mediante el parámetro sp_execute_external_script @input_data_1_partition_by_columns no se admite en esta versión de CTP.

## <a name="next-steps"></a>Pasos siguientes

+ [Cómo llamar a Java en SQL Server](howto-call-java-from-sql.md)
+ [Ejemplo de Java en SQL Server](java-first-sample.md)
+ [Tipos de datos de SQL Server y Java](java-sql-datatypes.md)