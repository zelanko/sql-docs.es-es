---
title: 'Arquitectura de extensibilidad para el lenguaje R y script de Python: SQL Server Machine Learning'
description: Compatibilidad con código externo para el motor de base de datos de SQL Server, con la arquitectura de doble para ejecutar el script de R y Python en datos relacionales.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3d4d8108fda500d48425abfb52fd9f72c6faa147
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963055"
---
# <a name="extensibility-architecture-in-sql-server-machine-learning-services"></a>Arquitectura de extensibilidad en SQL Server Machine Learning Services 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server tiene un marco de extensibilidad para la ejecución de scripts externos como R o Python en el servidor. Secuencia de comandos se ejecuta en un entorno de tiempo de ejecución de lenguaje como una extensión para el motor de base de datos principal. 

## <a name="background"></a>Información previa

El marco de extensibilidad se introdujo en SQL Server 2016 para admitir el runtime de R. SQL Server 2017 agrega compatibilidad con Python

El propósito del marco de extensibilidad es proporcionar una interfaz entre SQL Server y lenguajes de ciencia de datos como R y Python, lo que reduce la fricción al movimiento soluciones de ciencia de datos en producción y proteger los datos exponen durante el desarrollo proceso. Mediante la ejecución de un lenguaje de scripting de confianza dentro de un marco seguro administrado por SQL Server, los administradores de base de datos pueden mantener la seguridad al tiempo que permite a los científicos de datos acceso a datos empresariales.

El siguiente diagrama describe visualmente las oportunidades y los beneficios de la arquitectura extensible.

  ![Objetivos de la integración con SQL Server](../media/ml-service-value-add.png "valor agregado de Machine Learning Services")

Se puede ejecutar cualquier script de R o Python mediante una llamada a un procedimiento almacenado, y los resultados se devuelven como resultados tabulares directamente a SQL Server, lo que facilita a generar o consumir machine learning desde cualquier aplicación que pueda enviar una consulta SQL y controlar los resultados.

+ Ejecución de scripts externos está sujeto a la seguridad de datos de SQL Server, donde un usuario que ejecuta el script externo puede solo los datos de access está disponibles igualmente en una consulta SQL. Si se produce un error en una consulta debido a permisos insuficientes, la secuencia de comandos ejecutada por el mismo usuario también produciría un error por la misma razón. Seguridad de SQL Server se aplica en la tabla, la base de datos y el nivel de instancia. Los administradores de base de datos pueden administrar acceso de usuario, los recursos utilizados por los scripts externos y bibliotecas de código externo agregadas al servidor.  

+ Oportunidades de escalabilidad y optimización tienen una base dual: ganancias a través de la plataforma de base de datos (los índices de almacén de columnas, [regulación de recursos](../../advanced-analytics/r/resource-governance-for-r-services.md)) y mejoras de específica de la extensión cuando se usan las bibliotecas de Microsoft R y Python para los datos modelos de ciencia. Mientras que R es un único subproceso, las funciones de RevoScaleR son multiproceso, puede distribuir una carga de trabajo a través de varios núcleos.

+ Implementación usa las metodologías de SQL Server: procedimientos almacenados que se ajuste el script externo, embedded SQL o T-SQL funciones que realiza la llamada como PREDICT para devolver los resultados de los modelos de pronóstico que se guardan en el servidor de consultas.

+ Es necesario establecer los desarrolladores de R y Python con conocimientos en herramientas específicas y el IDE pueden escribir código en esas herramientas y, a continuación, trasladar código a SQL Server.

## <a name="architecture-diagram"></a>Diagrama de arquitectura

La arquitectura está diseñada para que ejecuten scripts externos en un proceso independiente de SQL Server, pero con los componentes que administran internamente la cadena de solicitudes de datos y las operaciones en SQL Server. Según la versión de SQL Server, las extensiones de lenguaje admitidos incluyen R y Python. 

  ![Arquitectura de componentes](../media/generic-architecture.png "arquitectura de componentes")

Los componentes incluyen una **Launchpad** servicio que se usa para invocar el lenguaje (R o Python), de los iniciadores específicos del idioma y la lógica de específicas de la biblioteca para la carga de intérpretes y bibliotecas. El iniciador carga un tiempo de ejecución de lenguaje, además de los módulos propietarios. Por ejemplo, si su código incluye funciones de RevoScaleR, cargaría un intérprete de RevoScaleR. **BxlServer** y **SQL Satellite** administrar la transferencia de datos y la comunicación con SQL Server.

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

El [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] es un servicio que administra y ejecuta scripts externos, similares a la forma en que el servicio de indización y consulta de texto completo inicia un host independiente para el procesamiento de consultas de texto completo. El servicio Launchpad puede empezar a solo los selectores de confianza publicados por Microsoft o que se han certificado por Microsoft que cumplan los requisitos de rendimiento y administración de recursos.

| Selectores de confianza | Extensión | Versiones de SQL Server |
|-------------------|-----------|---------------------|
| RLauncher.dll para el lenguaje R | [Extensión de R](extension-r.md) | SQL Server 2016, SQL Server 2017 |
| Pythonlauncher.dll para Python 3.5 | [Extensión de Python](extension-python.md) | SQL Server 2017 |

El servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] se ejecuta en su propia cuenta de usuario. Si cambia la cuenta que ejecuta Launchpad, asegúrese de hacerlo con el Administrador de configuración de SQL Server, para asegurarse de que los cambios se escriben en archivos relacionados.

Otro [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio se crea para cada instancia del motor de base de datos a la que ha agregado SQL Server Machine Learning Services. Hay un Launchpad servicio para cada instancia del motor de base de datos, por lo que si tiene varias instancias con compatibilidad con scripts externos, tendrá un servicio Launchpad para cada uno de ellos. Una instancia del motor de base de datos se enlaza al servicio Launchpad que se creó para él. Todas las invocaciones de script externo en un procedimiento almacenado o resultado de Transact-SQL en el servicio de SQL Server que llamar al servicio Launchpad creado para la misma instancia.

Para ejecutar tareas en un lenguaje compatible específico, Launchpad Obtiene una cuenta de trabajo protegidos del grupo e inicia un proceso satélite para administrar el tiempo de ejecución externo. Cada proceso satélite herede de la cuenta de usuario de Launchpad y usa esa cuenta de trabajo para la duración de ejecución del script. Si la secuencia de comandos utiliza procesos en paralelo, se crean bajo la cuenta de trabajo de la misma, una sola.

## <a name="bxlserver-and-sql-satellite"></a>BxlServer y SQL Satellite

**BxlServer** es un archivo ejecutable proporcionado por Microsoft que administra la comunicación entre SQL Server y Python o R. Crea los objetos de trabajo de Windows que se utilizan para contener sesiones de script externo, carpetas de trabajo seguras disposiciones para cada trabajo de script externo y usa SQL Satellite para administrar la transferencia de datos entre el tiempo de ejecución externo y SQL Server. Si ejecuta [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) mientras se ejecuta un trabajo, es posible que vea una o varias instancias de BxlServer.

De hecho, BxlServer es un complemento a un idioma que se ejecuta el entorno de tiempo que funciona con SQL Server para transferir datos y administrar tareas. BXL son las siglas de lenguaje de intercambio binario y hace referencia a los formatos de datos utilizados para mover datos eficazmente entre SQL Server y los procesos externos. BxlServer es también una parte importante de los productos relacionados como Microsoft R Client y Microsoft R Server.

**SQL Satellite** es una API de extensibilidad, incluido en el motor de base de datos a partir de SQL Server 2016, que es compatible con código externo o tiempos de ejecución externos implementados mediante C o C++.

BxlServer usa SQL Satellite para las tareas siguientes:

+ Leer datos de entrada
+ Escribir datos de salida
+ Obtener argumentos de entrada
+ Escribir argumentos de salida
+ Control de errores
+ Escribir STDOUT y STDERR de vuelta en el cliente

SQL Satellite usa un formato de datos personalizado que está optimizado para la transferencia rápida de datos entre SQL Server y los lenguajes de script externo. Realiza conversiones de tipos y define los esquemas de los conjuntos de datos de entrada y salida durante las comunicaciones entre SQL Server y el tiempo de ejecución de scripts externos.

SQL Satellite puede supervisarse mediante eventos extendidos (xEvents) de windows. Para obtener más información, consulte [eventos extendidos para R](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md) y [eventos extendidos para Python](../../advanced-analytics/python/extended-events-for-python.md).

## <a name="communication-channels-between-components"></a>Canales de comunicación entre componentes

Protocolos de comunicación entre los componentes y las plataformas de datos se describen en esta sección.

+ **TCP/IP**

  De forma predeterminada, las comunicaciones internas entre SQL Server y SQL Satellite usan TCP/IP.

+ **Canalizaciones con nombre**

  Transporte de datos internas entre el BxlServer y SQL Server mediante SQL Satellite usa un formato de datos comprimidos registrado para mejorar el rendimiento. Datos se intercambian entre los tiempos de ejecución de lenguaje y BxlServer en formato BXL, mediante canalizaciones con nombre.

+ **ODBC**

  Las comunicaciones entre los clientes de ciencia de datos externo y una instancia remota de SQL Server usan ODBC. La cuenta que envía los trabajos de la secuencia de comandos para SQL Server debe tener ambos permisos para conectarse a la instancia y ejecutar scripts externos.

  Además, dependiendo de la tarea, la cuenta que necesite estos permisos:

  + Leer los datos utilizados por el trabajo
  + Escribir datos en tablas: por ejemplo, al guardar los resultados a una tabla
  + Crear objetos de base de datos: por ejemplo, si se guarda el script externo como parte de un nuevo procedimiento almacenado.

  Cuando se usa SQL Server como contexto de proceso para el script que se ejecuta desde un cliente remoto y el ejecutable deben recuperar datos desde un origen externo, se usa ODBC para la escritura diferida. SQL Server asigna la identidad del usuario que emite el comando remoto a la identidad del usuario en la instancia actual y se ejecuta el comando ODBC con las credenciales del usuario. La cadena de conexión necesaria para realizar esta llamada ODBC se obtiene del código de cliente.

+ **RODBC (solo para R)** 

  Se pueden realizar llamadas ODBC adicionales dentro del script mediante **RODBC**. RODBC es un popular paquete de R que se usa para tener acceso a datos en bases de datos relacionales; Sin embargo, su rendimiento es normalmente más lento que los proveedores equiparables usados por SQL Server. Muchos scripts de R usan llamadas insertadas a RODBC como una manera de recuperar conjuntos de datos "secundarios" para su uso en el análisis. Por ejemplo, el procedimiento almacenado que entrena un modelo podría definir una consulta SQL para obtener datos para entrenar un modelo, pero podría usar una llamada RODBC insertada para obtener factores adicionales, realizar búsquedas u obtener nuevos datos de orígenes externos, como archivos de texto o Excel.

  El código siguiente muestra una llamada RODBC insertada en un script de R:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Otros protocolos**

  También pueden usar los procesos que necesitan para funcionar en "fragmentos" o transferir datos a un cliente remoto el [formato de archivo XDF](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). Transferencia de datos real es a través de blobs codificados.

## <a name="see-also"></a>Vea también

+ [Extensión de R en SQL Server](extension-r.md)
+ [Extensión de Python en SQL Server](extension-python.md)