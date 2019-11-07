---
title: Arquitectura de extensibilidad en extensiones de lenguaje de SQL Server
titleSuffix: SQL Server Language Extensions
description: Compatibilidad del código externo con el motor de base de datos de SQL Server, con una arquitectura dual para ejecutar lenguaje externo en datos relacionales.
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6cefa617dc6068f07b2cc2b684ce0442d7a438e8
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73589089"
---
# <a name="extensibility-architecture-in-sql-server-language-extensions"></a>Arquitectura de extensibilidad en extensiones de lenguaje de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Las extensiones de lenguaje de SQL Server tienen un marco de extensibilidad para ejecutar código externo, como Java, en el servidor. El código se ejecuta en un entorno de runtime de lenguaje como una extensión del motor de base de datos principal.

## <a name="background"></a>Información previa

El propósito del marco de extensibilidad es proporcionar una interfaz entre SQL Server y lenguajes externos como Java. Al ejecutar un lenguaje de confianza en un marco seguro que administra SQL Server, los administradores de bases de datos pueden mantener la seguridad y, al mismo tiempo, permitir que los científicos de datos accedan a los datos empresariales.

<!-- We need to get a diagram like the one below.
The following diagram visually describes opportunities and benefits of the extensible architecture.

  ![Goals of integration with SQL Server](../media/ml-service-value-add.png "Machine Learning Services Value Add")
-->

Cualquier lenguaje externo admitido se puede ejecutar si se llama a un procedimiento almacenado. En este caso, los resultados se devuelven como resultados tabulares directamente a SQL Server. Esto facilita el uso del lenguaje externo desde cualquier aplicación que pueda enviar una consulta SQL y controlar los resultados.

## <a name="architecture-diagrams"></a>Diagramas de arquitectura

La arquitectura está diseñada de modo que el código externo se ejecuta en un proceso independiente de SQL Server, pero con componentes que administran internamente la cadena de solicitudes de datos y operaciones en SQL Server. 
  
  ***Arquitectura de componentes en Windows:***

  ![Arquitectura de componentes en Windows](../media/generic-architecture-windows.png "Arquitectura de componentes en Windows")
  
  ***Arquitectura de componentes en Linux:***
  
  ![Arquitectura de componentes en Linux](../media/generic-architecture-linux.png "Arquitectura de componentes en Linux")
  
Los componentes incluyen un servicio **Launchpad** que se usa para invocar los runtimes externos (como Java) y la lógica específica de la biblioteca para cargar intérpretes y bibliotecas.

<a name="launchpad"></a>

## <a name="launchpad"></a>Launchpad

El [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] es un servicio que administra la duración, los recursos y los límites de seguridad del proceso externo que es responsable de la ejecución del script. Es similar a la forma en que el servicio de consulta e indexación de texto completo inicia un host independiente para procesar consultas de texto completo. El servicio Launchpad solo puede empezar iniciadores de confianza que publique Microsoft o que Microsoft haya certificado que cumplen los requisitos de rendimiento y administración de recursos.

| Iniciadores de confianza | Extensión | Versiones de SQL Server |
|-------------------|-----------|---------------------|
| JavaLauncher.dll para Java | Extensión de Java | SQL Server 2019 |

El servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] se ejecuta en **SQLRUserGroup**, que usa [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation) para aislar la ejecución.

Se crea un servicio de [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] independiente para cada instancia del motor de base de datos a la que ha agregado extensiones de lenguaje automático de SQL Server. Hay un servicio Launchpad para cada instancia del motor de base de datos, de modo que si tiene varias instancias que admiten scripts externos, contará con un servicio Launchpad para cada una de ellas. Una instancia del motor de base de datos se enlaza al servicio Launchpad creado para esta. Todas las invocaciones del script externo de un procedimiento almacenado o de T-SQL dan como resultado que el servicio SQL Server llama al servicio Launchpad creado para la misma instancia.

Para ejecutar tareas en un lenguaje específico compatible, Launchpad obtiene una cuenta de trabajo segura del grupo e inicia un proceso satélite para administrar el runtime externo. Cada proceso satélite hereda la cuenta de usuario de Launchpad y usa esa cuenta de trabajo mientras dure la ejecución del script. Si el script usa procesos paralelos, estos se crean en la misma cuenta de trabajo única.

## <a name="communication-channels-between-components"></a>Canales de comunicación entre componentes

En esta sección se describen los protocolos de comunicación entre componentes y plataformas de datos.

+ **TCP/IP**

  De forma predeterminada, la comunicación interna entre SQL Server y SQL Satellite usa TCP/IP.

+ **ODBC**

  Las comunicaciones entre los clientes de ciencia de datos externos y una instancia remota de SQL Server usan ODBC. La cuenta que envía los trabajos de script a SQL Server debe tener permisos para conectarse a la instancia y para ejecutar scripts externos.

  Además, en función de la tarea, la cuenta podría necesitar los siguientes permisos:

  + Lectura de datos que usa el trabajo.
  + Escritura de datos en tablas, por ejemplo, al guardar los resultados en una tabla.
  + Creación de objetos de base de datos, por ejemplo, si se guarda el script externo como parte de un procedimiento almacenado nuevo.

  Cuando se usa SQL Server como contexto de proceso para un script ejecutado desde un cliente remoto y el ejecutable debe recuperar datos de un origen externo, se usa ODBC para la escritura diferida. SQL Server asigna la identidad del usuario mediante la emisión del comando remoto a la identidad del usuario en la instancia actual y ejecuta el comando ODBC con las credenciales del usuario. La cadena de conexión necesaria para realizar esta llamada ODBC se obtiene del código de cliente.

+ **Otros protocolos**

  Los procesos que podrían necesitar trabajar en "fragmentos" o transferir datos de nuevo a un cliente remoto también pueden usar el [formato de archivo XDF](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf). La transferencia de datos real se realiza a través de blobs codificados.

## <a name="next-steps"></a>Pasos siguientes

+ [¿Qué son las extensiones de lenguaje?](../language-extensions-overview.md)
