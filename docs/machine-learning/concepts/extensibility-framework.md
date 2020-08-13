---
title: Arquitectura de extensibilidad
description: En este artículo se describe la arquitectura del marco de extensibilidad para ejecutar un script externo de R o Python en SQL Server Machine Learning Services. El script se ejecuta en un entorno de ejecución de lenguajes como extensión del motor de base de datos principal.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 14611369afe42da2e87aab87d675fd77e710c461
ms.sourcegitcommit: d1535944bff3f2580070cc036ece30f1d43ee2ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2020
ms.locfileid: "86406298"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>Arquitectura de extensibilidad en SQL Server Machine Learning Services 
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

En este artículo se describe la arquitectura del marco de extensibilidad para ejecutar un script externo de R o Python en SQL Server Machine Learning Services. El script se ejecuta en un entorno de ejecución de lenguajes como extensión del motor de base de datos principal.

## <a name="background"></a>Información previa

El marco de extensibilidad se ha introducido en SQL Server 2016 para admitir el entorno de ejecución de R con [R Services](../r/sql-server-r-services.md). SQL Server 2017 y versiones posteriores admiten Python con [Machine Learning Services](../sql-server-machine-learning-services.md).

El propósito del marco de extensibilidad es proporcionar una interfaz entre SQL Server y los lenguajes de ciencia de datos como R y Python. El objetivo es reducir la fricción al trasladar las soluciones de ciencia de datos al entorno de producción y proteger los datos expuestos durante el proceso de desarrollo. Al ejecutar un lenguaje de scripting de confianza en un marco seguro que administra SQL Server, los administradores de bases de datos pueden mantener la seguridad y, al mismo tiempo, permitir el acceso a los científicos de datos a los datos empresariales.

En el diagrama siguiente se describen visualmente las oportunidades y ventajas que ofrece la arquitectura extensible.

  ![Objetivos de la integración con SQL Server](../media/ml-service-value-add.png "Valor agregado de Machine Learning Services")

Un script externo se puede ejecutar llamando a un procedimiento almacenado. En este caso, los resultados se devuelven como resultados tabulares directamente a SQL Server. Esto facilita la generación o consumo de aprendizaje automático desde cualquier aplicación que pueda enviar una consulta SQL y controlar los resultados.

+ La ejecución de scripts externos está sujeta a la seguridad de datos de SQL Server. Un usuario que ejecuta un script externo solo puede tener acceso a los datos que estén igualmente disponibles en una consulta SQL. Si se produce un error en una consulta debido a permisos insuficientes, un script que ejecute el mismo usuario también producirá un error por el mismo motivo. La seguridad de SQL Server se aplica en el nivel de la tabla, la base de datos y la instancia. Los administradores de bases de datos pueden administrar el acceso de los usuarios, los recursos utilizados por los scripts externos y las bibliotecas de código externo agregadas al servidor.  

+ Las oportunidades de escala y optimización tienen una base dual: beneficios a través de la plataforma de base de datos (índices de almacén de columnas y [gobernanza de recursos](../../machine-learning/administration/resource-governor.md)) y mejoras específicas de la extensión, por ejemplo, al usar las bibliotecas de Microsoft de R y Python para los modelos de ciencia de datos. Mientras que R es de subproceso único, las funciones de RevoScaleR son multiproceso y pueden distribuir una carga de trabajo en varios núcleos.

+ La implementación utiliza las metodologías de SQL Server. Estas pueden ser procedimientos almacenados que encapsulen un script externo, consultas SQL incrustadas o consultas T-SQL que llamen a funciones como PREDICT para devolver los resultados de los modelos de previsión que se conserven en el servidor.

+ Los desarrolladores con aptitudes consolidadas en herramientas y IDE específicos pueden escribir código en esas herramientas y, después, portar el código a SQL Server.

## <a name="architecture-diagram"></a>Diagrama de la arquitectura

La arquitectura está diseñada de modo que los scripts externos se ejecuten en un proceso independiente de SQL Server, pero con componentes que administran internamente la cadena de solicitudes de datos y operaciones en SQL Server. En función de la versión de SQL Server, las extensiones de lenguaje compatibles incluyen [R](extension-r.md), [Python](extension-python.md) y lenguajes de terceros, como Java y .NET.

  ***Arquitectura de los componentes en Windows:***
  
  ![Arquitectura de los componentes de Windows](../media/generic-architecture-windows.png "Arquitectura de los componentes")
  
  ***Arquitectura de los componentes en Linux:***

  ![Arquitectura de los componentes de Linux](../media/generic-architecture-linux.png "Arquitectura de los componentes")
  
Los componentes incluyen un servicio **Launchpad** que se usa para invocar los entornos de ejecución externos y la lógica específica de la biblioteca a fin de cargar intérpretes y bibliotecas. El iniciador carga un entorno de ejecución de lenguajes, además de cualquier módulo de propietario. Por ejemplo, si el código incluye funciones de RevoScaleR, se cargará un intérprete de RevoScaleR. **BxlServer** y **SQL Satellite** administran la comunicación y la transferencia de datos con SQL Server. 

En Linux, SQL usa un servicio **Launchpad** a fin de comunicarse con un proceso de Launchpad independiente para cada usuario.

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] es un servicio que administra y ejecuta scripts externos, de modo similar a la forma en la que el servicio de consulta e indexación de texto completo inicia un host independiente para procesar consultas de texto completo. El servicio Launchpad solo puede empezar iniciadores de confianza publicados o certificados por Microsoft, lo que garantiza que cumplan los requisitos de rendimiento y administración de los recursos.

| Iniciadores de confianza | Extensión | Versiones de SQL Server |
|-------------------|-----------|---------------------|
| RLauncher.dll para el lenguaje R en Windows | [Extensión de R](extension-r.md) | SQL Server 2016 y posterior |
| Pythonlauncher.dll para Python 3.5 en Windows | [Extensión de Python](extension-python.md) | SQL Server 2017 y versiones posteriores |
| RLauncher.so para el lenguaje R en Linux | [Extensión de R](extension-r.md) | SQL Server 2019 y versiones posteriores |
| Pythonlauncher.so para Python 3.5 en Linux | [Extensión de Python](extension-python.md) | SQL Server 2019 y versiones posteriores |

El servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] se ejecuta en su propia cuenta de usuario. Si cambia la cuenta que ejecuta Launchpad, asegúrese de hacerlo mediante el Administrador de configuración de SQL Server para garantizar que los cambios se escriban en los archivos pertinentes.

En Windows, se crea un servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] independiente para cada instancia del motor de base de datos a la que se ha agregado SQL Server Machine Learning Services. Hay un servicio Launchpad para cada instancia del motor de base de datos, de modo que si tiene varias instancias que admitan scripts externos, contará con un servicio Launchpad para cada una de ellas. Una instancia del motor de base de datos se enlaza al servicio Launchpad creado para dicha instancia. Todas las invocaciones del script externo de un procedimiento almacenado o de T-SQL resultan en una llamada de SQL Server al servicio Launchpad creado para la misma instancia.

Para ejecutar tareas en un lenguaje específico admitido, Launchpad obtiene una cuenta de trabajo segura del grupo e inicia un proceso satélite para administrar el entorno de ejecución externo. Cada proceso satélite hereda la cuenta de usuario de Launchpad y usa esa cuenta de trabajo mientras dure la ejecución del script. Si el script usa procesos paralelos, estos se crean en la misma cuenta de trabajo única.

En Linux, solo se admite una instancia del motor de base de datos, y hay un servicio Launchpad enlazado a la instancia. Cuando se ejecuta un script, el servicio Launchpad inicia un proceso de Launchpad independiente con la cuenta de usuario con pocos privilegios **mssql_satellite**. Cada proceso satélite hereda la cuenta de usuario mssql_satellite de Launchpad y la usa durante la ejecución del script.

## <a name="bxlserver-and-sql-satellite"></a>BxlServer y SQL Satellite

**BxlServer** es un ejecutable proporcionado por Microsoft que administra la comunicación entre SQL Server y el entorno de ejecución de lenguajes. Crea los objetos de trabajo de Windows para Windows, o bien los espacios de nombres para Linux, que se usan para contener sesiones de scripts externos. También aprovisiona carpetas de trabajo seguras para cada trabajo de script externo y utiliza SQL Satellite a fin de administrar la transferencia de datos entre el entorno de ejecución externo y SQL Server. Si ejecuta el [Explorador de procesos](https://technet.microsoft.com/sysinternals/processexplorer.aspx) mientras se está ejecutando un trabajo, es posible que vea una o varias instancias de BxlServer.

En efecto, BxlServer es un complemento de un entorno de ejecución de lenguajes que funciona con SQL Server para transferir datos y administrar tareas. BXL son las siglas en inglés de "lenguaje de intercambio binario" y hace referencia al formato de datos que se usa para mover datos de manera eficiente entre SQL Server y procesos externos. BxlServer también es una parte importante de los productos relacionados, como Microsoft R Client y Microsoft R Server.

**SQL Satellite** es una nueva API de extensibilidad incluida en el motor de base de datos que admite código externo o entornos de ejecución externos implementados mediante C o C++.

BxlServer usa SQL Satellite para las tareas siguientes:

+ Leer datos de entrada
+ Escritura de datos de salida
+ Obtener argumentos de entrada
+ Escribir argumentos de salida
+ Control de errores
+ Escribir STDOUT y STDERR de vuelta en el cliente

SQL Satellite usa un formato de datos personalizado que está optimizado para una transferencia de datos rápida entre SQL Server y lenguajes de script externos. Realiza conversiones de tipos y define los esquemas de los conjuntos de datos de entrada y salida durante las comunicaciones entre SQL Server y el entorno de ejecución de scripts externos.

SQL Satellite puede supervisarse mediante eventos extendidos de Windows (xEvents). Para obtener más información, vea [Eventos extendidos para SQL Server Machine Learning Services](../../machine-learning/administration/extended-events.md).

## <a name="communication-channels-between-components"></a>Canales de comunicación entre componentes

En esta sección se describen los protocolos de comunicación entre los componentes y las plataformas de datos.

+ **TCP/IP**

  De forma predeterminada, la comunicación interna entre SQL Server y SQL Satellite usa TCP/IP.

+ **Canalizaciones con nombre**

  El transporte de datos internos entre BxlServer y SQL Server a través de SQL Satellite usa un formato de datos comprimidos de propietario para mejorar el rendimiento. Los datos se intercambian entre los entornos de ejecución de lenguajes y BxlServer en formato BXL mediante canalizaciones con nombre.

+ **ODBC**

  Las comunicaciones entre los clientes de ciencia de datos externos y una instancia remota de SQL Server usan ODBC. La cuenta que envía los trabajos de script a SQL Server debe tener permisos para conectarse a la instancia y para ejecutar scripts externos.

  Además, en función de la tarea, la cuenta podría necesitar los siguientes permisos:

  + Lectura de datos que usa el trabajo.
  + Escritura de datos en tablas; por ejemplo, al guardar los resultados en una tabla.
  + Creación de objetos de bases de datos: por ejemplo, si se guarda el script externo como parte de un procedimiento almacenado nuevo.

  Cuando se usa SQL Server como contexto de proceso para un script ejecutado desde un cliente remoto y el ejecutable debe recuperar datos de un origen externo, se usa ODBC para la escritura diferida. SQL Server asigna la identidad del usuario mediante la emisión del comando remoto a la identidad del usuario en la instancia actual y ejecuta el comando ODBC con las credenciales del usuario. La cadena de conexión necesaria para realizar esta llamada ODBC se obtiene del código de cliente.

+ **RODBC (solo R)** 

  Se pueden realizar llamadas ODBC adicionales dentro del script mediante **RODBC**. RODBC es un popular paquete de R que se usa para obtener acceso a datos de bases de datos relacionales, pero su rendimiento suele ser más lento que el de proveedores equiparables que usa SQL Server. Muchos scripts de R usan llamadas insertadas a RODBC como una manera de recuperar conjuntos de datos "secundarios" para su uso en el análisis. Por ejemplo, el procedimiento almacenado que entrena un modelo podría definir una consulta SQL para obtener datos para entrenar un modelo, pero podría usar una llamada RODBC insertada para obtener factores adicionales, realizar búsquedas u obtener nuevos datos de orígenes externos, como archivos de texto o Excel.

  El código siguiente muestra una llamada RODBC insertada en un script de R:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Otros protocolos**

  Los procesos que puede que necesiten trabajar en "fragmentos" o transferir datos de nuevo a un cliente remoto también pueden utilizar el [formato de archivo XDF](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). La transferencia de datos real se realiza a través de blobs codificados.

## <a name="see-also"></a>Consulte también

+ [Extensión de R en SQL Server](extension-r.md)
+ [Extensión de Python en SQL Server](extension-python.md)