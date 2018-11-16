---
title: R Services en SQL Server 2016 | Microsoft Docs
description: R en SQL Server para las tareas de R integradas en datos relacionales, incluyendo la ciencia de datos y modelado estadístico, análisis predictivo, visualización de datos y mucho más.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/10/2018
ms.topic: overview
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 17d0aa51d43ad9592a075ae91be88c857035b15f
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51659934"
---
# <a name="r-services-in-sql-server-2016"></a>R Services en SQL Server 2016
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R Services es un complemento a una instancia de motor de base de datos de SQL Server 2016, utilizado para ejecutar código R y funciones en SQL Server. Código se ejecuta en un marco de extensibilidad, aislada de los procesos del motor principal, pero totalmente disponible para datos relacionales como procedimientos almacenados, como script de Transact-SQL que contiene instrucciones de R o como código de R que contiene la instrucción T-SQL. 

R Services incluye una distribución de base de R, que se superpone con paquetes de R enterprise de Microsoft para que pueda cargar y procesar grandes cantidades de datos en varios núcleos y agregar los resultados en una única salida consolidada. Funciones de R y los algoritmos de Microsoft están diseñados para el escalado y utilidad: entrega de análisis predictivo, modelado estadístico, visualizaciones de datos y algoritmos en un producto de servidor comercial ingeniería de aprendizaje de automático de vanguardia y compatible con Microsoft. 

Las bibliotecas de R incluyen RevoScaleR, MicrosoftML y otros. Puesto que R Services está integrado con el motor de base de datos, puede mantener análisis cerca de los datos y eliminar los costos y riesgos de seguridad asociados con el movimiento de datos.

> [!Note]
> Se cambió el nombre de R Services en SQL Server 2017 que [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md), que refleja la adición de Python.

## <a name="components"></a>Components

SQL Server 2016 solo es R. En la tabla siguiente se describe las características de SQL Server 2016.

| Componente | Descripción |
|-----------|-------------|
| Servicio Launchpad de SQL Server | Un servicio que administra las comunicaciones entre los tiempos de ejecución de R externo y la instancia de SQL Server. |
| Paquetes de R | [**RevoScaleR** ](revoscaler-overview.md) es la biblioteca principal para funciones escalables de R. en esta biblioteca se encuentran entre los más usados. Muchas formas de modelado y análisis y manipulación, resumen estadístico, visualización y transformaciones de datos se encuentran en estas bibliotecas. Además, las funciones de estas bibliotecas distribución automáticamente las cargas de trabajo entre núcleos disponibles para el procesamiento en paralelo, con la capacidad de trabajar en fragmentos de datos que se coordina y administra el motor de cálculo.  <br/>[**MicrosoftML (R)** ](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) agrega los algoritmos de aprendizaje automático para crear modelos personalizados para el análisis de opiniones, análisis de imágenes y análisis de texto. <br/>[**sqlRUtils** ](generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md) proporciona funciones auxiliares para colocar los scripts de R en un procedimiento almacenado de T-SQL, registrar un procedimiento almacenado con una base de datos y ejecutando el procedimiento almacenado desde un entorno de desarrollo de R.<br/>[**olapR** ](how-to-create-mdx-queries-using-olapr.md) sirve para especificar las consultas MDX en R.|
| Microsoft R Open (MRO) | [**MRO** ](https://mran.microsoft.com/open) es la distribución de código abierto de Microsoft de R. Se incluyen el paquete y el intérprete. Utilice siempre la versión de MRO instalado el programa de instalación. |
| Herramientas de R | Símbolos del sistema y las ventanas de la consola de R son herramientas estándares en una distribución de R.  |
| Ejemplos de R y las secuencias de comandos |  Paquetes de código abierto R y RevoScaleR incluyen conjuntos de datos integrados para que se puede crear y ejecutar el script con datos previamente instalados |
| Modelos previamente entrenados de R | Modelos previamente entrenados se crean para casos de uso específicos y mantenidos por el equipo de ingeniería de ciencia de datos de Microsoft. Puede usar los modelos previamente entrenados como-es la puntuación de opiniones positivas y negativas en texto, o bien detectar características de imágenes, con nuevas entradas de datos que proporcione. Los modelos de ejecución de R Services, pero no se puede instalar a través del programa de instalación de SQL Server. Para obtener más información, consulte [instalar previamente entrenado modelos de machine learning en SQL Server](../install/sql-pretrained-models-install.md). |

## <a name="using-r-services"></a>Con R Services

Los programadores y analistas suelen tengan código que se ejecutan en una instancia de SQL Server local. Adición de Machine Learning Services y habilitar la ejecución de scripts externos, ofrece la posibilidad de ejecutar código R en modalidades de SQL Server: ajuste el script en los procedimientos almacenados, almacenar modelos en una tabla de SQL Server o combinar funciones de Transact-SQL y R en las consultas.

El enfoque más común para realizar análisis en bases de datos es usar [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), pasando el script de R como un parámetro de entrada.

Las interacciones de cliente-servidor clásico es otro enfoque. Desde cualquier estación de trabajo cliente que tenga un IDE, puede instalar [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)y, a continuación, escribir código que inserta la ejecución (denominados un *contexto de cálculo remoto*) a los datos y las operaciones a una instancia de SQL remoto Servidor. 

Por último, si está utilizando un [servidor independiente](r-server-standalone.md) y Developer edition, puede crear soluciones en una estación de trabajo cliente usando las mismas bibliotecas y los intérpretes y, a continuación, implementar código de producción en SQL Server Machine Learning Servicios (en bases de datos). 

## <a name="how-to-get-started"></a>Cómo empezar a trabajar

Comience con el programa de instalación, adjuntar los archivos binarios a la herramienta de desarrollo que prefiera y escribir la primera secuencia de comandos.

**Paso 1:** instalar y configurar el software. 

+ [Instalar SQL Server 2016 R Services (en bases de datos)](../install/sql-r-services-windows-install.md)

**Paso 2:** Obtenga experiencia práctica mediante uno de estos tutoriales:

+ [Tutorial: Obtenga información sobre los análisis en bases de datos mediante R](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Tutorial: Tutorial de extremo a otro con R](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)

**Paso 3:** agregar los paquetes de R favoritos y usarlas junto con los paquetes proporcionados por Microsoft

+ [Administración de paquetes de R para SQL Server](install-additional-r-packages-on-sql-server.md)


## <a name="see-also"></a>Vea también

 [Instalar SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
