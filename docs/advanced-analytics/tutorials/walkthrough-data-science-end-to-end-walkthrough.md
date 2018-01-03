---
title: Tutorial de ciencia de datos to-end para R y SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 08/22/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: edd76ae9-4125-45a8-bf42-47a85b9d9a32
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 9d6654109e3cb5ff2e2c174dc37fd02bfc02dcb3
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="end-to-end-data-science-walkthrough-for-r-and-sql-server"></a>Tutorial de ciencia de datos to-end para R y SQL Server

En este tutorial, desarrolle una solución end-to-end para el modelado de predicción basado en Microsoft R con SQL Server 2016 o 2017 de SQL Server.

Este tutorial se basa en un conjunto de datos público conocido, el conjunto de datos de los taxis de Nueva York. Usar una combinación de código de R, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos y funciones SQL personalizadas que se va a crear un modelo de clasificación que indique la probabilidad de que el controlador puede obtener una sugerencia durante un viaje taxi determinado. También implementa el modelo de R para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y usar datos de servidor para generar puntuaciones que se basa en el modelo.

En este ejemplo se puede extender a todos los tipos de problemas de la vida real, como la predicción de respuestas de los clientes para campañas de ventas o predecir gastos o asistencia a eventos. Dado que el modelo se puede invocar desde un procedimiento almacenado, puede insertar fácilmente en una aplicación.

Dado que el tutorial está diseñado para presentar a los desarrolladores de R [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], R se usa siempre que sea posible. Sin embargo, esto no significa que R es necesariamente la mejor herramienta para cada tarea. En muchos casos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría proporcionar un mejor rendimiento, especialmente en tareas como la agregación de datos e ingeniería de características.  Esas tareas pueden beneficiarse de las nuevas características de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], como los índices de almacén de columnas con optimización para memoria. Intentamos señalar posibles optimizaciones a lo largo de la forma.

> [!NOTE]
> El tutorial se desarrolló y probó originalmente en SQL Server 2016. Sin embargo, capturas de pantalla y los procedimientos se han actualizado para usar la versión más reciente de SQL Server Management Studio, que funciona con SQL Server 2017.

## <a name="overview"></a>Información general

Estimado tiempos no incluyen el programa de instalación. Para obtener más información, consulte [requisitos previos para el tutorial](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).

|Lista de temas|Tiempo estimado|
|-|------------------------------|
|[Preparar los datos del tutorial de R](../tutorials/walkthrough-prepare-the-data.md) <br /><br />Obtener los datos usados para generar un modelo. Descargar un conjunto de datos público y cargarlo en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|30 minutos|
|[Explorar los datos con SQL](../tutorials/walkthrough-view-and-explore-the-data.md) <br /><br />Comprender los datos con resúmenes y herramientas de SQL.|10 minutos|
|[Resumir los datos con R](../tutorials/walkthrough-view-and-summarize-data-using-r.md) <br /><br />Usar R para explorar los datos y generar resúmenes.|10 minutos|
|[Crear gráficos de uso de R en SQL Server](../tutorials/walkthrough-create-graphs-and-plots-using-r.md) <br /><br />Crear gráficos en contextos de proceso local y remoto mezclando R y SQL.|10 minutos|
|[Crear características de datos mediante R y T-SQL)](../tutorials/walkthrough-create-data-features.md) <br /><br />Realizar el diseño de las características con las funciones personalizadas en R y [!INCLUDE[tsql](../../includes/tsql-md.md)]. Comparar el rendimiento de R y T-SQL para las tareas de características. |10 minutos|
|[Generar un modelo de R y guardarlo en SQL Server](../tutorials/walkthrough-build-and-save-the-model.md) <br /><br />Entrenar y ajustar un modelo predictivo. Evaluar el rendimiento del modelo. Este tutorial crea un modelo de clasificación. Trazar la exactitud del modelo mediante R.|15 minutos|
|[Implementar el modelo de R mediante SQL Server](../tutorials/walkthrough-deploy-and-use-the-model.md) <br /><br />Implementar el modelo en producción, guardándolo en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Llamar al modelo desde un procedimiento almacenado para generar predicciones.|10 minutos|

### <a name="intended-audience"></a>Destinatarios

Este tutorial está pensado para desarrolladores de R o SQL. Proporciona una introducción a cómo se puede integrar R en flujos de trabajo empresariales mediante [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  Debe estar familiarizado con las operaciones de base de datos, como crear tablas y bases de datos, la importación de datos y ejecutar consultas.

+ Se incluyen todos los scripts SQL y R.
+ Tendrá que modificar las cadenas en las secuencias de comandos, para que se ejecute en su entorno. Puede hacerlo con cualquier editor de código, como [código de Visual Studio](https://code.visualstudio.com/Download).

### <a name="prerequisites"></a>Prerequisites

+ Debe tener acceso a una instancia de SQL Server 2016 o una versión de evaluación de SQL Server 2017.
+ Al menos una instancia en el equipo de SQL Server debe tener instalado [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].
+ Si desea ejecutar comandos de R desde un equipo remoto, como un equipo portátil o en otro equipo en red, debe instalar las bibliotecas de Microsoft R Open. Puede instalar Microsoft R Client o Microsoft R Server. El equipo remoto debe ser capaz de conectarse a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.
+ Si tiene que colocar el cliente y servidor en el mismo equipo, asegúrese de instalar un conjunto independiente de las bibliotecas de R de Microsoft para su uso en el envío del script de R desde un cliente "remoto". No utilice las bibliotecas de R que se instalan para su uso por la instancia de SQL Server para este propósito.

Para obtener más información acerca de cómo configurar estos entornos de cliente y servidor, consulte [requisitos previos de tutorial de ciencia de datos de R y SQL Server](../tutorials/walkthrough-prerequisites-for-data-science-walkthroughs.md).

## <a name="next-lesson"></a>Lección siguiente

[Preparar los datos del tutorial de R](../tutorials/walkthrough-prepare-the-data.md)
