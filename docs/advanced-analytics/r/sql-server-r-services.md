---
title: R Services en SQL Server 2016
description: R en SQL Server para las tareas integradas de R en datos relacionales, como ciencia de datos y modelado estadístico, análisis predictivo, visualización de datos, etc.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 32487d8c1a6c87c9ad916e4cfd517f9ba4cba6e2
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469905"
---
# <a name="r-services-in-sql-server-2016"></a>R Services en SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R Services es un complemento de una instancia del motor de base de datos SQL Server 2016, que se usa para ejecutar código R y funciones en SQL Server. El código se ejecuta en un marco de extensibilidad, aislado de los procesos principales del motor, pero está totalmente disponible para los datos relacionales como procedimientos almacenados, como un script de T-SQL que contiene instrucciones de R o como código de R que contiene T-SQL. 

R Services incluye una distribución base de R, que se superpone con paquetes de R de empresa de Microsoft para que pueda cargar y procesar grandes cantidades de datos en varios núcleos y agregar los resultados en una sola salida consolidada. Las funciones y los algoritmos de R de Microsoft están diseñados para la escala y la utilidad, que ofrecen análisis predictivo, modelos estadísticos, visualizaciones de datos y algoritmos de aprendizaje automático de vanguardia en un producto de servidor comercial y compatible con Microsoft. 

Las bibliotecas de R incluyen [**RevoScaleR**](ref-r-revoscaler.md), [**MicrosoftML (R)** ](ref-r-microsoftml.md)y otras. Dado que R Services está integrado con el motor de base de datos, puede mantener el análisis cerca de los datos y eliminar los costos y riesgos de seguridad asociados al movimiento de datos.

> [!Note]
> Se ha cambiado el nombre de R Services en SQL Server 2017 y versiones posteriores a [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md), lo que refleja la adición de Python.

## <a name="components"></a>Componentes

SQL Server 2016 es solo R. En la tabla siguiente se describen las características de SQL Server 2016.

| Componente | Descripción |
|-----------|-------------|
| Servicio de SQL Server Launchpad | Servicio que administra las comunicaciones entre los tiempos de ejecución de R externos y la instancia de SQL Server. |
| Paquetes de R | [**RevoScaleR**](ref-r-revoscaler.md) es la biblioteca principal para R. las funciones escalables de esta biblioteca están entre las más usadas. En estas bibliotecas se encuentran las transformaciones y la manipulación de datos, el resumen estadístico, la visualización y muchas formas de modelado y análisis. Además, las funciones de estas bibliotecas distribuyen automáticamente las cargas de trabajo entre los núcleos disponibles para el procesamiento en paralelo, con la capacidad de trabajar en fragmentos de datos que el motor de cálculo coordina y administra.  <br/>[**MicrosoftML (R)** ](ref-r-microsoftml.md) agrega algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de texto, el análisis de imágenes y el análisis de opiniones. <br/>[**sqlRUtils**](ref-r-sqlrutils.md) proporciona funciones auxiliares para colocar scripts de R en un procedimiento almacenado de T-SQL, registrar un procedimiento almacenado con una base de datos y ejecutar el procedimiento almacenado desde un entorno de desarrollo de R.<br/>[**olapr**](ref-r-olapr.md) es para especificar consultas MDX en R.|
| Microsoft R Open (MRO) | [**MRO**](https://mran.microsoft.com/open) es la distribución de código abierto de Microsoft de R. Se incluyen el paquete y el intérprete. Use siempre la versión de MRO instalada por el programa de instalación. |
| Herramientas de R | Las ventanas de la consola de r y los símbolos del sistema son herramientas estándar en una distribución de R.  |
| Ejemplos y scripts de R |  Los paquetes de código abierto R y RevoScaleR incluyen conjuntos de datos integrados para que pueda crear y ejecutar scripts con datos preinstalados. |
| Modelos previamente entrenados en R | Los modelos previamente entrenados se crean para casos de uso específicos y los mantiene el equipo de ingeniería de ciencia de datos de Microsoft. Puede usar los modelos previamente entrenados tal cual para puntuar la opinión positiva negativa en el texto o para detectar características en las imágenes, con las nuevas entradas de datos que proporcione. Los modelos se ejecutan en R Services, pero no se pueden instalar a través del programa de instalación de SQL Server. Para obtener más información, consulte [instalación de modelos de aprendizaje automático entrenados previamente en SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-r-services"></a>Uso de R Services

Los desarrolladores y analistas suelen tener código que se ejecuta sobre una instancia de SQL Server local. Al agregar Machine Learning Services y habilitar la ejecución de scripts externos, tiene la capacidad de ejecutar código de R en SQL Server modalidades: encapsular script en procedimientos almacenados, almacenar modelos en una tabla de SQL Server o combinar funciones de T-SQL y R en consultas.

El enfoque más común para el análisis en bases de datos es el uso de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), pasando el script de R como parámetro de entrada.

Las interacciones de cliente y servidor clásicas son otro enfoque. Desde cualquier estación de trabajo cliente que tenga un IDE, puede instalar [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)y, a continuación, escribir código que inserte la ejecución (denominada " *contexto de cálculo remoto*") en datos y operaciones en un SQL Server remoto. 

Por último, si usa un [servidor independiente](r-server-standalone.md) y la edición para desarrolladores, puede compilar soluciones en una estación de trabajo cliente con las mismas bibliotecas e intérpretes y, a continuación, implementar el código de producción en SQL Server Machine Learning Services (en base de datos). 

## <a name="how-to-get-started"></a>Cómo empezar

Comience con el programa de instalación, adjunte los archivos binarios a su herramienta de desarrollo favorita y escriba el primer script.

**Paso 1:** Instalar y configurar el software. 

+ [Instalación de 2016 SQL Server R Services (en bases de datos)](../install/sql-r-services-windows-install.md)

**Paso 2:** Obtenga experiencia práctica con cualquiera de estos tutoriales:

+ [Tutorial: Aprenda a usar análisis en bases de datos con R](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Tutorial: Tutorial de un extremo a otro con R](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**Paso 3:** Agregue sus paquetes de R favoritos y úselos junto con los paquetes proporcionados por Microsoft

+ [Administración de paquetes de R para SQL Server](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>Vea también

 [Instalación de SQL Server R Services de 2016](../install/sql-r-services-windows-install.md)
