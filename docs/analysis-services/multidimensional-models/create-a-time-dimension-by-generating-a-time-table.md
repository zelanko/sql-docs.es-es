---
title: Crear una dimensión de tiempo generando una tabla de tiempos | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d35cf55f64b977e952b57416a31c35cd669fc468
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867072"
---
# <a name="create-a-time-dimension-by-generating-a-time-table"></a>Crear una dimensión de tiempo generando una tabla de tiempos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], puede utilizar el Asistente para dimensiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para crear una dimensión de tiempo cuando ninguna tabla de tiempos está disponible en la base de datos de origen. Para ello, seleccione una de las opciones siguientes en la página **Seleccionar método de creación** :  
  
-   **Generar una tabla de tiempos en el origen de datos** : seleccione esta opción cuando tenga el permiso para crear objetos en el origen de datos subyacente. A continuación, el asistente generará una tabla de tiempos y la almacenará en el origen de datos. El asistente crea entonces la dimensión de tiempo de esa tabla de tiempos.  
  
-   **Generar una tabla de tiempos en el servidor** : seleccione esta opción cuando no tenga permiso para crear objetos en el origen de datos subyacente. A continuación, el asistente generará y almacenará una tabla en el servidor en lugar de realizarlo en el origen de datos. (La dimensión creada a partir de una tabla de tiempos en el servidor se denomina *dimensión de tiempo de servidor*). El asistente crea a continuación la dimensión de tiempo de servidor a partir de esa tabla.  
  
 Cuando cree una dimensión de tiempo, debe especificar los períodos de tiempo y las fechas de inicio y de finalización de la dimensión. El asistente utiliza los períodos de tiempo especificados para crear los atributos de tiempo. Al procesar la dimensión, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera y almacena los datos necesarios para admitir las fechas y períodos de tiempo especificados. El asistente usa los atributos creados para una dimensión de tiempo para recomendar las jerarquías de la dimensión. Las jerarquías reflejan las relaciones entre distintos períodos de tiempo y tienen en cuenta distintos calendarios. Por ejemplo, en una jerarquía de calendario estándar, se muestra el nivel Weeks bajo el nivel Years, pero no bajo el nivel Months, ya que las semanas se dividen de forma regular en años pero no en meses. En cambio, en una jerarquía de calendario de informes o de fabricación, las semanas se dividen de forma regular en meses, por lo que el nivel Weeks se muestra bajo el nivel Months.  
  
## <a name="define-time-periods"></a>Definir períodos de tiempo  
 Use la página **Definir períodos de tiempo** del asistente para especificar el intervalo de fechas que desea incluir en la dimensión. Por ejemplo, puede elegir un intervalo que comience el primero de enero del primer año de los datos y que finalice uno o dos años después del año actual (para permitir transacciones futuras). Las transacciones que queden fuera del intervalo no aparecerán o, si lo hacen, aparecerán como miembros desconocidos de la dimensión en función del valor de la propiedad **UnknownMemberVisible** de la dimensión. También puede cambiar el primer día de la semana que se usará en los datos (el valor predeterminado es Domingo).  
  
 Seleccione los períodos de tiempo que se utilizarán cuando el asistente crea jerarquías que se apliquen a datos como Años, Semestres, Trimestres, Cuatrimestres, Meses, Diez días, Semanas o Fecha. Deberá seleccionar siempre al menos el período de tiempo Fecha. El atributo Date es el atributo clave de la dimensión, por lo que la dimensión no puede funcionar sin él.  
  
 Seleccione junto a **Idioma de los nombres de miembros de tiempo**el idioma que desea utilizar para etiquetar los miembros de la dimensión.  
  
 Una vez creada la dimensión de tiempo basada en un intervalo de fechas, puede utilizar el Diseñador de dimensiones para agregar o quitar atributos de tiempo. Dado que el atributo Date es el atributo clave de la dimensión, no podrá quitarse de la dimensión. Para ocultar el atributo Date a los usuarios, puede cambiar la propiedad **AttributeHierarchyVisible** a **False**.  
  
## <a name="select-calendars"></a>Seleccionar calendarios  
 El calendario estándar de 12 meses (gregoriano), que comienza el primero de enero y finaliza el 31 de diciembre, se incluye siempre al crear una dimensión de tiempo. En la página **Seleccionar calendarios** del asistente, puede especificar calendarios adicionales en los que se basan las jerarquías de la dimensión. Para obtener descripciones de los tipos de calendarios, vea [Crear una dimensión de tipo Date](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md).  
  
 Según los períodos de tiempo seleccionados en la página **Definir períodos de tiempo** del asistente, las selecciones de calendario determinan los atributos que se crean en la dimensión. Por ejemplo, si selecciona los períodos de tiempo **Año** y **Trimestre** en la página **Definir períodos de tiempo** del asistente y selecciona **Calendario fiscal** en la página **Seleccionar calendarios** , se crearán los atributos FiscalYear, FiscalQuarter y FiscalQuarterOfYear para el calendario fiscal.  
  
 El asistente también crea jerarquías específicas para el calendario que se componen de los atributos creados para el calendario. En cada calendario, los niveles de las jerarquías se acumulan en el nivel superior. Por ejemplo, en el calendario estándar de 12 meses, el asistente crea una jerarquía de Years y Weeks o Years y Months. Sin embargo, las semanas no están contenidas de forma uniforme en los meses de un calendario estándar, por lo que no hay una jerarquía de Years, Months y Weeks. Por el contrario, las semanas de un calendario de informes o de fabricación se dividen de forma uniforme en meses, por lo que en estos calendarios las semanas se acumulan en meses.  
  
## <a name="completing-the-dimension-wizard"></a>Completar el Asistente para dimensiones  
 En la página **Finalización del asistente** , podrá revisar los atributos y jerarquías creados en el asistente y asignar un nombre a la dimensión de tiempo. Haga clic en **Finalizar** para completar el asistente y crear la dimensión. Una vez haya finalizado la dimensión, podrá cambiarla con el Diseñador de dimensiones.  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Crear una dimensión de tipo Date](../../analysis-services/multidimensional-models/database-dimensions-create-a-date-type-dimension.md)   
 [Propiedades de la dimensión de base de datos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties.md)   
 [Relaciones de dimensión](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)   
 [Crear una dimensión generando una tabla que no sea de tiempos en el origen de datos](../../analysis-services/multidimensional-models/create-a-dimension-by-generating-a-non-time-table-in-the-data-source.md)  
  
  
