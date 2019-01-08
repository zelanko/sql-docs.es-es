---
title: Crear inteligencia empresarial (BI) flujos de trabajo con R - SQL Server Machine Learning Services
description: Admiten escenarios de integración de combinación de inteligencia empresarial (BI) y el lenguaje R en SQL Server y SQL Server Integration Services (SSIS).
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 32dfb3317cb790c19289ab02362bf8ee765e5259
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432738"
---
# <a name="creating-bi-workflows-with-r"></a>Creación de flujos de trabajo de BI con R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Una base de datos relacional es una tecnología altamente optimizada que ofrece soluciones escalables de procesamiento de transacciones, almacenamiento y consulta de datos.

En cambio, tradicionalmente las soluciones de R han recurrido a importar datos desde diversos orígenes, a menudo en formato CSV, para que siga explorando y modelando los datos. Tales prácticas no solo son poco eficaces, sino que entrañan riesgos.

En este artículo se describe escenarios de integración para R con SQL Server que evitar los riesgos comunes y los riesgos de seguridad que pueden producirse si se desarrollan soluciones de aprendizaje automático fuera de la base de datos.

También se describen ejemplos de cómo las aplicaciones de inteligencia empresarial, en particular, Integration Services y Reporting Services, pueden interactuar con el código de R y consumir datos o los gráficos generados por R.

Se aplica a: SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

## <a name="bring-compute-power-to-the-data"></a>Traiga la potencia de proceso a los datos

Ha sido un objetivo de diseño clave de la integración de aprendizaje automático con SQL Server genere análisis cerca de los datos. Esto ofrece varias ventajas:

+ Seguridad de datos. Volver a poner más cerca de R para el origen de datos evita el movimiento de datos de una pérdida de tiempo o no seguros.

+ Velocidad. Las bases de datos están optimizadas para operaciones basadas en conjuntos. Las recientes innovaciones realizadas en bases de datos como tablas en memoria los resúmenes y agregaciones con suma y están a un complemento perfecto para ciencia de datos.

+ Facilidad de integración e implementación. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el punto central de operaciones para muchas otras tareas de administración de datos y aplicaciones. Con datos que residen en la base de datos o el almacén de informes, se asegura de que los datos utilizados por las soluciones de aprendizaje automático son coherentes y están actualizados. 

+ Eficiencia en la nube y locales. En lugar de procesar datos en R, puede confiar en las canalizaciones de datos empresariales incluidos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y Azure Data Factory. Los informes de análisis o de resultados son sencillos a través de Power BI o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

Si usan la combinación adecuada de SQL y R para distintas tareas de procesamiento y análisis de datos, los científicos de datos y los desarrolladores lograrán ser más productivos.

## <a name="use-integration-services-for-data-transformation-and-automation"></a>Usar Integration Services para datos de transformación y automatización

Los flujos de trabajo de ciencia de datos son tremendamente iterativos y conllevan una enorme transformación de los datos, como los ajustes de escala, las agregaciones, el cálculo de probabilidades y cambiar los atributos de nombre y combinarlos. Los científicos de datos están acostumbrados a realizar muchas de estas tareas en R, Python u otro lenguaje. Pero ejecutar estos flujos de trabajo con datos empresariales requiere una integración perfecta con procesos y herramientas de ETL.

Como [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite realizar operaciones complejas en R a través de Transact-SQL y de procedimientos almacenados, se pueden integrar las tareas específicas de R con los procesos de ETL existentes sin tener que emplear tiempo en volver a desarrollar. En lugar de seguir una cadena de tareas de gran cantidad de memoria de R, preparación de datos puede optimizarse mediante las herramientas más eficaces, incluyendo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Estas son algunas ideas sobre cómo automatizar el procesamiento de datos y modelado de canalizaciones mediante [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Use [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tareas para crear características de los datos necesarios en la base de datos SQL
+ Usar bifurcaciones condicionales para alternar el contexto de ejecución de trabajos de R
+ Ejecutar trabajos de R que generan sus propios datos en la base de datos y compartir datos con aplicaciones
+ Cuando se usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cargue el script de R guardado en una variable de texto y ejecutarlo en SQL Server

### <a name="examples"></a>Ejemplos

[Incorporación de operatividad a su proyecto de aprendizaje automático mediante SQL Server 2016 SSIS y R Services](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  

Esta entrada de blog muestra las técnicas básicas para manipular el código de R con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: 

+ Llamar a R mediante la tarea Ejecutar SQL, para generar datos y guardarlos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

+ Usar un procedimiento almacenado para entrenar un modelo de R y almacenarlo en la base de datos

+ Realizar la puntuación en el modelo mediante las tareas Script y Ejecutar SQL

##  <a name="bkmk_ssrs"></a> Usar Reporting Services para la visualización

Aunque R puede crear gráficos y visualizaciones interesantes, no se integra bien con orígenes de datos externos, lo que significa que cada gráfico debe representarse individualmente. El uso compartido también puede ser difícil.

Con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], se pueden ejecutar operaciones complejas en R a través de los procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)], que muchas herramientas de informes empresariales pueden usar sin problemas, como [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y Power BI.

+ Visualizar objetos gráficos devueltos desde un script de R con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]
+ Usar la tabla de Power BI

### <a name="examples"></a>Ejemplos

[R Graphics Device for Microsoft Reporting Services (SSRS)](https://rgraphicsdevice.codeplex.com/) (Dispositivo gráfico de R para Microsoft Reporting Services [SSRS])

Este proyecto de CodePlex proporciona el código para ayudarle a crear un elemento de informe personalizado que representa la salida gráfica de R como una imagen que puede usarse en informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  Mediante el elemento de informe personalizado se puede:

+ Publicar gráficos y trazados creados con el dispositivo gráfico de R en paneles de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]

+ Pasar parámetros de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a trazados de R

> [!NOTE]
> Para este ejemplo, el código que admite el dispositivo de gráficos de R para Reporting Services debe instalarse en el servidor de Reporting Services, así como en Visual Studio. También se requiere la configuración y compilación manual.
