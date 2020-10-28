---
title: ¿Qué son las extensiones de lenguaje de SQL Server?
titleSuffix: ''
description: Las extensiones de lenguaje son una característica de SQL Server que se usa para ejecutar código externo. En SQL Server 2019, se admiten Java, R y Python. Los datos relacionales se pueden usar en el código externo mediante el uso del marco de extensibilidad.
author: dphansen
ms.author: davidph
ms.date: 10/07/2020
ms.topic: overview
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c4482adb86f9a2f205bd64044a18f342cf3e13c5
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/17/2020
ms.locfileid: "92154946"
---
# <a name="what-is-sql-server-language-extensions"></a>¿Qué son las extensiones de lenguaje de SQL Server?
[!INCLUDE [SQL Server 2019 and later](../includes/applies-to-version/sqlserver2019.md)]

Las extensiones de lenguaje son una característica de SQL Server que se usa para ejecutar código externo. Los datos relacionales se pueden usar en el código externo mediante el uso del [marco de extensibilidad](concepts/extensibility-framework.md).

En SQL Server 2019, se admiten Java, R y Python.

> [!NOTE]
> Para ejecutar Python o R en SQL Server, vea la documentación de [Aprendizaje automático de SQL](../machine-learning/index.yml). Con SQL Server 2019 y versiones posteriores, puede usar un tiempo de ejecución personalizado de Python y R con extensiones de lenguaje. Para más información, vea [Tiempo de ejecución personalizado de Python](../machine-learning/install/custom-runtime-python.md) y [Tiempo de ejecución personalizado de R](../machine-learning/install/custom-runtime-r.md).

## <a name="what-you-can-do-with-language-extensions"></a>Qué puede hacer con las extensiones de lenguaje

Las extensiones de lenguaje usan el marco de extensibilidad para ejecutar código externo. La ejecución del código está aislada de los procesos principales del motor, pero está totalmente integrada con la ejecución de consultas de SQL Server. Puede ejecutar código en el origen de los datos, lo que elimina la necesidad de extraer datos a través de la red.

Los lenguajes externos se definen con [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md). El procedimiento almacenado del sistema [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) se usa como interfaz para ejecutar el código.

Las extensiones de lenguaje proporcionan varias ventajas:

+ Seguridad de datos. La ejecución del lenguaje externo más cerca del origen de datos evita que se muevan los datos de forma excesiva o no segura.
+ Velocidad. Las bases de datos están optimizadas para operaciones basadas en conjuntos. Las innovaciones recientes en las bases de datos, como las tablas en memoria, permiten realizar resúmenes y agregaciones con suma rapidez, y son un complemento perfecto para la ciencia de datos.
+ Facilidad de implementación e integración. [!INCLUDE [ssNoVersion](../includes/ssnoversion-md.md)] es el punto central de operaciones para muchas otras tareas y aplicaciones de administración de datos. Si usa los datos que residen en la base de datos, tendrá la garantía de que los datos usados por la extensión de lenguaje son coherentes y están actualizados.

## <a name="next-steps"></a>Pasos siguientes

+ Instalación de un [tiempo de ejecución personalizado de Python para SQL Server](../machine-learning/install/custom-runtime-python.md)
+ Instalación de un [tiempo de ejecución personalizado de R para SQL Server](../machine-learning/install/custom-runtime-r.md)
+ Instalación de [extensiones de lenguaje de SQL Server en Windows](install/windows-java.md) o en [Linux](../linux/sql-server-linux-setup-language-extensions-java.md)
+ Instalación del [SDK de extensibilidad de Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md)
