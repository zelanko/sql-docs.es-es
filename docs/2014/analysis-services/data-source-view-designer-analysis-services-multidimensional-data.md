---
title: Diseñador de vistas del origen de datos (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.f1
helpviewer_keywords:
- Data Source View Designer
ms.assetid: 6f40a074-761f-440b-a999-09b755bd86ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd19f3a7f4978d2f8bcbd8e62cdf542e05437519
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175172"
---
# <a name="data-source-view-designer-analysis-services---multidimensional-data"></a>Diseñador de vistas del origen de datos (Analysis Services - Datos multidimensionales)
  Una vista del origen de datos (DSV) es una vista lógica de un origen de datos relacional externo utilizado para crear cubos y dimensiones en un modelo multidimensional.

 Una vez generada una DSV, puede utilizar el **Diseñador de vistas del origen de datos** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para trabajar directamente en la DSV, lo que puede ser útil si el origen de datos subyacente son elementos de datos que faltan y que son necesarios en un modelo multidimensional.

 Para abrir el **Diseñador de vistas del origen de datos** :

-   Haga doble clic en una vista del origen de datos en el **Explorador de soluciones**.

-   Haga clic con el botón derecho en una vista del origen de datos en el **Explorador de soluciones** y seleccione **Abrir** o **Diseñador de vistas**.

 El **Diseñador de vistas del origen de datos** contiene una barra de herramientas, un diagrama que muestra los objetos y las relaciones de la DSV, un panel de tablas que muestra las tablas y las consultas con nombre en orden alfabético, y un panel Organizador de diagramas que se utiliza para crear y ver diagramas específicos de la DSV. Puede hacer clic con el botón secundario en una tabla o una relación para tener acceso a comandos contextuales.

 ![Diseñador de vistas del origen de datos](media/ssas-dsvdesigner.PNG "Diseñador de vistas del origen de datos")

 Como mínimo, una DSV muestra las tablas de base de datos relacional que se utilizarán para rellenar objetos del modelo durante el procesamiento. Se genera una DSV, normalmente mediante el Asistente para vistas del origen de datos. Las tablas, columnas y relaciones de la DSV se convierten en la base de las dimensiones y medidas de un cubo. Una vez creada la DSV, puede utilizar el Diseñador de vistas del origen de datos para modificarla.

 La mayoría de los desarrolladores de Analysis Services utilizan una DSV generada tal cual, con pocas personalizaciones. Esto es especialmente frecuente si el origen de datos procede de una vista de una base de datos de SQL Server. En este caso, quizás prefiera administrar las relaciones de datos y los cálculos en una vista T-SQL en lugar de en una DSV de Analysis Services. Sin embargo, si no es el propietario de la base de datos subyacente, puede modificar la DSV de Analysis Services para desarrollar aún más las estructuras de datos utilizadas en el modelo.

## <a name="tasks-in-data-source-view-designer"></a>Tareas del Diseñador de vistas del origen de datos
 Con el Diseñador de vistas del origen de datos, puede realizar las siguientes modificaciones en una DSV:

|||
|-|-|
|Cambiar el nombre de columnas o tablas, o crear nuevas columnas calculadas. Por ejemplo, concatenar un nombre y un apellido en una nueva columna con el nombre completo.|[Definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)|
|Agregar manualmente relaciones entre tablas|[Definir relaciones lógicas en una vista del origen de datos &#40;Analysis Services&#41;](multidimensional-models/define-logical-relationships-in-a-data-source-view-analysis-services.md)|
|Crear una consulta con nombre para definir un nuevo objeto basándose en una consulta de T-SQL.|[Definir consultas con nombre en una vista del origen de datos &#40;Analysis Services&#41;](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)|
|Explorar los datos subyacentes para ver los valores de datos reales representados por objetos del modelo.<br /><br /> La exploración de datos permite inspeccionar visualmente y copiar los datos devueltos desde la tabla o consulta dimensional subyacente. De forma predeterminada, la exploración de datos usa la metodología de muestreo de primeros puestos, con un número de muestras de 5000, pero puede modificar estos valores.|[Explorar los datos de una vista del origen de datos &#40;Analysis Services&#41;](multidimensional-models/explore-data-in-a-data-source-view-analysis-services.md)|
|Crear un diagrama de todas las tablas y relaciones de una DSV o de algunas de ellas|[Trabajar con diagramas en el diseñador de vistas del origen de datos &#40;Analysis Services&#41;](multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)|

## <a name="see-also"></a>Consulte también
 [Vistas del origen de datos en modelos multidimensionales](multidimensional-models/data-source-views-in-multidimensional-models.md) [Agregar o quitar tablas o vistas en una vista del origen de datos &#40;Analysis Services&#41;](multidimensional-models/adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services.md)


