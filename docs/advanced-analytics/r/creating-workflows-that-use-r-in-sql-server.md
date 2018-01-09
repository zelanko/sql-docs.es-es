---
title: Crear flujos de trabajo de BI con R | Documentos de Microsoft
ms.custom: SQL2016_New_Updated
ms.date: 04/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 34c3b1c2-97db-4cea-b287-c7f4fe4ecc1b
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 624510d814a2b91fdb61d6090abbc673d704d262
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="creating-bi-workflows-with-r"></a>Crear flujos de trabajo de BI con R

Una base de datos relacional es una tecnología altamente optimizada que ofrece soluciones escalables de procesamiento de transacciones, almacenamiento y consulta de datos.

En cambio, tradicionalmente generalmente se basaban soluciones en R sobre cómo importar datos de varios orígenes, a menudo, en formato CSV, para realizar el modelado y la exploración de datos adicional. Tales prácticas no solo son poco eficaces, sino que entrañan riesgos.

En este tema se describe los escenarios de integración para R con SQL Server que evitar los riesgos y los riesgos de seguridad que se pueden producir si se desarrollan soluciones de aprendizaje de máquina fuera de la base de datos comunes.

También se describen algunos ejemplos de aplicaciones de business intelligence, en particular, Integration Services y Reportng Services, pueden interactuar con el código de R y consumir datos o los gráficos generados mediante R.

Se aplica a: servicios de aprendizaje de automático de SQL Server 2016 R Services, SQL Server de 2017

## <a name="bring-compute-power-to-the-data"></a>Poner la capacidad de proceso a los datos

Un objetivo clave del diseño de la integración de aprendizaje automático con SQL Server ha sido llevan el análisis cerca de los datos. Esto proporciona varias ventajas:

+ Seguridad de datos. Incluir R más cerca en el origen de datos evita el movimiento de datos innecesarios o insegura.

+ Velocidad. Las bases de datos están optimizadas para operaciones basadas en conjuntos. Las recientes innovaciones realizadas en bases de datos como tablas en memoria realizar resúmenes y agregaciones con suma y son un complemento perfecto para ciencia de datos.

+ Facilidad de implementación y la integración. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]es el punto central de operaciones para muchas otras tareas de administración de datos y aplicaciones. Mediante el uso de datos que residen en la base de datos o almacenamiento de informes, se asegura de que los datos utilizados por las soluciones de aprendizaje automático están coherente y actualizado. 

+ Eficacia en la nube y locales. En lugar de procesar datos en R, puede confiar en las canalizaciones de datos empresariales incluidos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y Azure Data Factory. Los informes de análisis o de resultados son sencillos a través de Power BI o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

Si usan la combinación adecuada de SQL y R para distintas tareas de procesamiento y análisis de datos, los científicos de datos y los desarrolladores lograrán ser más productivos.

## <a name="use-integration-services-for-data-transformation-and-automation"></a>Usar servicios de integración para datos de transformación y automatización

Los flujos de trabajo de ciencia de datos son tremendamente iterativos y conllevan una enorme transformación de los datos, como los ajustes de escala, las agregaciones, el cálculo de probabilidades y cambiar los atributos de nombre y combinarlos. Los científicos de datos están acostumbrados a realizar muchas de estas tareas en R, Python u otro lenguaje. Pero ejecutar estos flujos de trabajo con datos empresariales requiere una integración perfecta con procesos y herramientas de ETL.

Como [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] permite realizar operaciones complejas en R a través de Transact-SQL y de procedimientos almacenados, se pueden integrar las tareas específicas de R con los procesos de ETL existentes sin tener que emplear tiempo en volver a desarrollar. En su lugar de llevar a cabo una cadena de tareas que utilizan mucha memoria en R, preparación de los datos se puede optimizar mediante las herramientas más eficaces, incluidos los [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Estos son algunos ideass de cómo automatizar los datos de procesamiento de un dmodeling canalizaciones mediante [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ Use [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tareas para crear características de datos necesarios en la base de datos SQL
+ Usar bifurcaciones condicionales para alternar el contexto de ejecución de trabajos de R
+ Ejecutar trabajos de R que generan sus propios datos en la base de datos y compartir datos con aplicaciones
+ Cuando se usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cargue el script de R guardado en una variable de texto y lo ejecuta en SQL Server

### <a name="examples"></a>Ejemplos

[Incorporación de operatividad a su proyecto de aprendizaje automático mediante SQL Server 2016 SSIS y R Services](https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/)  

Esta entrada de blog muestra las técnicas básicas para manipular el código de R con [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]: 

+ Llamar a R mediante la tarea Ejecutar SQL, para generar datos y guardar en[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

+ Usar un procedimiento almacenado para entrenar un modelo de R y almacenarlo en la base de datos

+ Realizar la puntuación en el modelo mediante las tareas Script y Ejecutar SQL

##  <a name="bkmk_ssrs"></a>Usar Reporting Services para la visualización

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
> En este ejemplo, el código que es compatible con el dispositivo de gráficos de R para Reporting Services debe estar instalado en el servidor de Reporting Services, así como en Visual Studio. También se requiere la configuración y compilación manual.
