---
title: ¿Qué son las extensiones de lenguaje?
titleSuffix: SQL Server Language Extensions
description: Obtenga información acerca de las extensiones de lenguaje de SQL Server 2019 (versión preliminar) que ejecutan scripts externos en SQL Server.
author: dphansen
ms.author: davidph
ms.date: 11/04/2019
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 15ff0339a487ecebdca23057bfce9053b5efca2e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73589029"
---
# <a name="what-is-sql-server-language-extensions-preview"></a>¿Qué son las extensiones de lenguaje de SQL Server (versión preliminar)?
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Las extensiones de lenguaje son una característica de SQL Server que se usa para ejecutar código externo. Los datos relacionales se pueden usar en el código externo mediante el uso del [marco de extensibilidad](concepts/extensibility-framework.md).

En SQL Server 2019, se admite Java. El runtime predeterminado de Java es Zulu Open JRE. También puede usar otro JRE o SDK de Java.

## <a name="what-you-can-do-with-language-extensions"></a>Qué puede hacer con las extensiones de lenguaje

Las extensiones de lenguaje usan el marco de extensibilidad para ejecutar código externo. La ejecución del código está aislada de los procesos principales del motor, pero está totalmente integrada con la ejecución de consultas de SQL Server. Permiten ejecutar código donde residen los datos, lo que elimina la necesidad de extraer los datos a través de la red.

Los lenguajes externos se definen con [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql). El procedimiento almacenado del sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) se usa como interfaz para ejecutar el código.

Las extensiones de lenguaje proporcionan varias ventajas:

+ Seguridad de datos. La ejecución del lenguaje externo más cerca del origen de datos evita que se muevan los datos de forma excesiva o no segura.
+ Velocidad. Las bases de datos están optimizadas para operaciones basadas en conjuntos. Las innovaciones recientes en las bases de datos, como las tablas en memoria, permiten realizar resúmenes y agregaciones con suma rapidez, y son un complemento perfecto para la ciencia de datos.
+ Facilidad de implementación e integración. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] es el punto central de operaciones para muchas otras tareas y aplicaciones de administración de datos. El uso de los datos que residen en la base de datos, garantiza que la información que usa Java es coherente y está actualizada.

## <a name="how-to-get-started"></a>Introducción

### <a name="step-1-install-the-software"></a>Paso 1: Instalar el software

+ [Extensiones de lenguaje de SQL Server en Windows](install/install-sql-server-language-extensions-on-windows.md)
+ [Extensiones de lenguaje de SQL Server en Linux](../linux/sql-server-linux-setup-language-extensions.md)

### <a name="step-2-configure-a-development-tool"></a>Paso 2: Configurar una herramienta de desarrollo

Normalmente, los desarrolladores escriben código en su propia estación de trabajo de desarrollo o en su portátil. Con las extensiones de lenguaje de SQL Server, no es necesario cambiar este proceso. Una vez completada la instalación, puede ejecutar código Java en SQL Server.

+ **Use el IDE que prefiera** para desarrollar código Java.

+ **Instale el [SDK de extensibilidad para Java de Microsoft](how-to/extensibility-sdk-java-sql-server.md)** para ejecutar código Java en SQL Server.

+ **Use [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)** para ejecutar código externo en SQL Server.

+ **Use el procedimiento almacenado del sistema [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)** para ejecutar el código Java en SQL Server.

### <a name="step-3-write-your-first-code"></a>Paso 3: Escribir el primer código

Ejecute código Java desde el script de T-SQL:

+ [Tutorial: Expresiones regulares con Java](tutorials/search-for-string-using-regular-expressions-in-java.md)

## <a name="limitations"></a>Limitaciones

+ El número de valores de los búferes de entrada y salida no puede ser superior a `MAX_INT (2^31-1)` ya que es el número máximo de elementos que se pueden asignar en una matriz en Java.

## <a name="next-steps"></a>Pasos siguientes

+ Instalación de [extensiones de lenguaje de SQL Server en Windows](install/install-sql-server-language-extensions-on-windows.md) o [en Linux](../linux/sql-server-linux-setup-language-extensions.md)
+ Instalación del [SDK de extensibilidad de Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md)
