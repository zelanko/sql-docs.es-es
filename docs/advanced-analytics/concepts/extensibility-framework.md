---
title: Arquitectura de extensibilidad para el lenguaje R y el script de Python
description: Compatibilidad de código externo con el motor de base de datos de SQL Server, con una arquitectura dual para ejecutar scripts de R y Python en datos relacionales.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a5c49172ed23867f95e383878f792092bd762177
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470457"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>Arquitectura de extensibilidad en SQL Server Machine Learning Services 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server tiene un marco de extensibilidad para ejecutar scripts externos como R o Python en el servidor. El script se ejecuta en un entorno de tiempo de ejecución de lenguaje como una extensión del motor de base de datos principal. 

## <a name="background"></a>Información previa

El marco de extensibilidad se presentó en SQL Server 2016 para admitir el tiempo de ejecución de R. SQL Server 2017 agrega compatibilidad con Python

El propósito de la plataforma de extensibilidad es proporcionar una interfaz entre SQL Server y los lenguajes de ciencia de datos como R y Python, lo que reduce la fricción al trasladar las soluciones de ciencia de datos a producción y proteger los datos expuestos durante el desarrollo. Procese. Al ejecutar un lenguaje de scripting de confianza en un marco seguro administrado por SQL Server, los administradores de bases de datos pueden mantener la seguridad y, al mismo tiempo, permitir el acceso a los científicos de datos a los datos empresariales.

En el diagrama siguiente se describen visualmente las oportunidades y ventajas de la arquitectura extensible.

  ![Objetivos de la integración con SQL Server](../media/ml-service-value-add.png "Machine Learning Services agregar valor")

Cualquier script de R o Python se puede ejecutar mediante una llamada a un procedimiento almacenado, y los resultados se devuelven como resultados tabulares directamente a SQL Server, lo que facilita la generación o el consumo de aprendizaje automático desde cualquier aplicación que pueda enviar una consulta SQL y controlar los resultados.

+ La ejecución de scripts externos está sujeta a SQL Server seguridad de datos, donde un usuario que ejecuta un script externo solo puede tener acceso a datos que están igualmente disponibles en una consulta SQL. Si se produce un error en una consulta debido a permisos insuficientes, el script ejecutado por el mismo usuario también producirá un error por el mismo motivo. SQL Server seguridad se aplica en el nivel de la tabla, la base de datos y la instancia. Los administradores de bases de datos pueden administrar el acceso de los usuarios, los recursos utilizados por los scripts externos y las bibliotecas de código externo agregadas al servidor.  

+ Las oportunidades de escalado y optimización tienen dos bases: beneficios a través de la plataforma de base de datos (índices de almacén de columnas, [regulación de recursos](../../advanced-analytics/r/resource-governance-for-r-services.md)) y mejoras específicas de la extensión cuando se usan bibliotecas de Microsoft para R y Python para modelos de ciencia de datos. Mientras que R es de subproceso único, las funciones de RevoScaleR son multiproceso y pueden distribuir una carga de trabajo en varios núcleos.

+ La implementación usa metodologías de SQL Server: procedimientos almacenados que ajustan las consultas de script externo, SQL incrustado o T-SQL que llaman a funciones como PREDICT para devolver los resultados de los modelos de previsión que se conservan en el servidor.

+ Los desarrolladores de R y Python con conocimientos establecidos en herramientas y IDE específicos pueden escribir código en esas herramientas y, a continuación, trasladar el código a SQL Server.

## <a name="architecture-diagram"></a>Diagrama de arquitectura

La arquitectura está diseñada de modo que los scripts externos se ejecuten en un proceso independiente de SQL Server, pero con componentes que administran internamente la cadena de solicitudes de datos y operaciones en SQL Server. En función de la versión de SQL Server, las extensiones de lenguaje compatibles incluyen R y Python. 

  ![Arquitectura de componentes](../media/generic-architecture.png "Arquitectura de componentes")

Los componentes incluyen un servicio **Launchpad** que se usa para invocar iniciadores específicos del lenguaje (R o Python), el lenguaje y la lógica específica de la biblioteca para cargar intérpretes y bibliotecas. El iniciador carga un tiempo de ejecución de idioma, además de cualquier módulo de propiedad. Por ejemplo, si el código incluye funciones de RevoScaleR, se cargará un intérprete de RevoScaleR. **BxlServer** y **SQL Satellite** administran la comunicación y la transferencia de datos con SQL Server.

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Es un servicio que administra y ejecuta scripts externos, de forma similar al modo en que el servicio de indización y consulta de texto completo inicia un host independiente para procesar las consultas de texto completo. El servicio Launchpad solo puede iniciar iniciadores de confianza publicados por Microsoft o que Microsoft ha certificado como requisitos para la administración de recursos y rendimiento.

| Iniciadores de confianza | Extensión | SQL Server versiones |
|-------------------|-----------|---------------------|
| RLauncher. dll para el lenguaje R | [Extensión de R](extension-r.md) | SQL Server 2016, SQL Server 2017 |
| Pythonlauncher. dll para Python 3,5 | [Extensión de Python](extension-python.md) | SQL Server 2017 |

El servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] se ejecuta en su propia cuenta de usuario. Si cambia la cuenta que ejecuta Launchpad, asegúrese de hacerlo mediante Administrador de configuración de SQL Server, para asegurarse de que los cambios se escriben en los archivos relacionados.

Se crea [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] un servicio independiente para cada instancia del motor de base de datos a la que haya agregado SQL Server Machine Learning Services. Hay un servicio Launchpad para cada instancia del motor de base de datos, por lo que si tiene varias instancias con compatibilidad con scripts externos, tendrá un servicio Launchpad para cada una de ellas. Una instancia del motor de base de datos se enlaza al servicio Launchpad creado para ella. Todas las invocaciones del script externo de un procedimiento almacenado o de T-SQL dan como resultado el servicio SQL Server que llama al servicio Launchpad creado para la misma instancia.

Para ejecutar tareas en un idioma específico compatible, Launchpad obtiene una cuenta de trabajo segura del grupo e inicia un proceso satélite para administrar el tiempo de ejecución externo. Cada proceso satélite hereda la cuenta de usuario de Launchpad y usa esa cuenta de trabajo mientras dure la ejecución del script. Si el script usa procesos paralelos, se crean en la misma cuenta de trabajo única.

## <a name="bxlserver-and-sql-satellite"></a>BxlServer y SQL Satellite

**BxlServer** es un ejecutable proporcionado por Microsoft que administra la comunicación entre SQL Server y Python o R. Crea los objetos de trabajo de Windows que se usan para contener sesiones de script externo, aprovisiona carpetas de trabajo seguras para cada trabajo de script externo y utiliza SQL Satellite para administrar la transferencia de datos entre el tiempo de ejecución externo y el SQL Server. Si ejecuta el [Explorador de procesos](https://technet.microsoft.com/sysinternals/processexplorer.aspx) mientras se ejecuta un trabajo, podría ver una o varias instancias de BxlServer.

En efecto, BxlServer es un complemento de un entorno de tiempo de ejecución de lenguaje que funciona con SQL Server para transferir datos y administrar tareas. BXL representa el lenguaje de intercambio binario y hace referencia al formato de datos que se usa para trasladar datos de forma eficaz entre SQL Server y procesos externos. BxlServer también es una parte importante de los productos relacionados, como Microsoft R Client y Microsoft R Server.

**SQL Satellite** es una API de extensibilidad que se incluye en el motor de base de datos a partir de SQL Server 2016, que admite código externo o tiempos C++de ejecución externos implementados mediante C o.

BxlServer usa SQL Satellite para las tareas siguientes:

+ Leer datos de entrada
+ Escribir datos de salida
+ Obtener argumentos de entrada
+ Escribir argumentos de salida
+ Control de errores
+ Escribir STDOUT y STDERR de vuelta en el cliente

SQL Satellite usa un formato de datos personalizado que está optimizado para la transferencia de datos rápida entre SQL Server y los lenguajes de script externos. Realiza conversiones de tipos y define los esquemas de los conjuntos de datos de entrada y salida durante las comunicaciones entre SQL Server y el tiempo de ejecución del script externo.

El satélite de SQL se puede supervisar mediante el uso de eventos extendidos de Windows (xEvents). Para obtener más información, consulte [Extended Events for R](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md) y [Extended Events for Python](../../advanced-analytics/python/extended-events-for-python.md).

## <a name="communication-channels-between-components"></a>Canales de comunicación entre componentes

En esta sección se describen los protocolos de comunicación entre componentes y plataformas de datos.

+ **TCP/IP**

  De forma predeterminada, las comunicaciones internas entre SQL Server y el satélite de SQL usan TCP/IP.

+ **Canalizaciones con nombre**

  El transporte de datos interno entre BxlServer y SQL Server a través de SQL Satellite usa un formato de datos de propietario y comprimido para mejorar el rendimiento. Los datos se intercambian entre los tiempos de ejecución del lenguaje y BxlServer en formato BXL mediante canalizaciones con nombre.

+ **ODBC**

  Las comunicaciones entre los clientes externos de ciencia de datos y una instancia de SQL Server remota usan ODBC. La cuenta que envía los trabajos de script a SQL Server debe tener ambos permisos para conectarse a la instancia y ejecutar scripts externos.

  Además, en función de la tarea, la cuenta podría necesitar estos permisos:

  + Leer datos usados por el trabajo
  + Escribir datos en tablas: por ejemplo, al guardar los resultados en una tabla
  + Crear objetos de base de datos: por ejemplo, si se guarda el script externo como parte de un nuevo procedimiento almacenado.

  Cuando se usa SQL Server como el contexto de cálculo para el script ejecutado desde un cliente remoto, y el ejecutable debe recuperar datos de un origen externo, se usa ODBC para la reescritura. SQL Server asigna la identidad del usuario que emite el comando remoto a la identidad del usuario en la instancia actual y ejecuta el comando ODBC con las credenciales del usuario. La cadena de conexión necesaria para realizar esta llamada ODBC se obtiene del código de cliente.

+ **RODBC (solo R)** 

  Se pueden realizar llamadas ODBC adicionales dentro del script mediante **RODBC**. RODBC es un conocido paquete de R que se usa para tener acceso a los datos de las bases de datos relacionales. sin embargo, su rendimiento suele ser más lento que los proveedores comparables usados por SQL Server. Muchos scripts de R usan llamadas insertadas a RODBC como una manera de recuperar conjuntos de datos "secundarios" para su uso en el análisis. Por ejemplo, el procedimiento almacenado que entrena un modelo podría definir una consulta SQL para obtener datos para entrenar un modelo, pero podría usar una llamada RODBC insertada para obtener factores adicionales, realizar búsquedas u obtener nuevos datos de orígenes externos, como archivos de texto o Excel.

  El código siguiente muestra una llamada RODBC insertada en un script de R:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Otros protocolos**

  Los procesos que podrían necesitar trabajar en "fragmentos" o transferir datos de nuevo a un cliente remoto también pueden usar el [formato de archivo XDF](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). La transferencia de datos real se realiza a través de blobs codificados.

## <a name="see-also"></a>Vea también

+ [Extensión de R en SQL Server](extension-r.md)
+ [Extensión de Python en SQL Server](extension-python.md)