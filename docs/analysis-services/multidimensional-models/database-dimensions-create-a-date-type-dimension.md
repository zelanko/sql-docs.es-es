---
title: "Crear una dimensión de tipo de fecha | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- time dimensions [Analysis Services]
- dimensions [Analysis Services], time
- adding time intelligence
- server time dimensions [Analysis Services]
- calendars [Analysis Services]
- time intelligence [Analysis Services]
ms.assetid: 6d692856-4b01-4dca-a650-f97ac220c114
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 52470e4818d24aeb2288d41f60114f040e669cd6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="database-dimensions---create-a-date-type-dimension"></a>Dimensiones de base de datos: crear una dimensión de tipo de fecha
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], una dimensión de tiempo es un tipo de dimensión cuyos atributos representan periodos de tiempo, como horas, semestres, trimestres, meses y días. Los periodos en una dimensión de tiempo proporcionan niveles de granularidad basados en tiempo para la elaboración de análisis e informes. Los atributos se organizan en jerarquías y la granularidad de la dimensión de tiempo se determina en gran parte según los requisitos empresariales y de informes de los datos históricos. Por ejemplo, la mayoría de datos financieros y de ventas en las aplicaciones de Business Intelligence utilizan una granularidad mensual o trimestral.  
  
 Normalmente, los cubos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incorporan algún formato de dimensión de tiempo. Un cubo puede incluir más de una dimensión de tiempo o varias jerarquías de la misma dimensión de tiempo, según la granularidad de los datos y los requisitos de informes. Sin embargo, no todos los cubos necesitan una dimensión de tiempo. Algunas aplicaciones OLAP, como la estimación de costos basada en la actividad, no requieren una dimensión de tiempo, porque la estimación de costos de una dimensión basada en actividades no se basa en el tiempo, sino en la actividad.  
  
## <a name="dimension-structure"></a>Estructura de dimensión  
 La estructura de dimensión de una dimensión de tiempo depende del modo en que el origen de datos subyacente almacena la información del periodo de tiempo. Esta diferencia en el almacenamiento genera dos tipos básicos de dimensiones de tiempo:  
  
 Dimensión de tiempo  
 Las dimensiones de tiempo se parecen a otras dimensiones en que una tabla de dimensiones proporciona los atributos de la dimensión. Cada columna de la tabla principal de dimensiones define un atributo para un periodo de tiempo especificado.  
  
 Al igual que otras dimensiones, la tabla de hechos tiene una relación de clave externa con la tabla de dimensiones de la dimensión de tiempo. El atributo clave de una dimensión de tiempo se basa en una clave de entero o en el nivel más bajo de detalle, como la fecha, que aparece en la tabla principal de dimensiones.  
  
 Dimensión de tiempo del servidor  
 Si no dispone de una tabla de dimensiones a la que enlazar atributos relacionados con el tiempo, puede hacer que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] defina una dimensión de tiempo del servidor basada en periodos de tiempo. Para definir las jerarquías, niveles y miembros representados por la dimensión de tiempo del servidor, seleccione periodos estándar al crear la dimensión.  
  
 Los atributos de una dimensión de tiempo de servidor tienen enlaces especiales a atributos de tiempo. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa los tipos de atributos relacionados con fechas, como Year, Month o Day, para definir los miembros de los atributos de una dimensión de tiempo.  
  
 Después de incluir la dimensión de tiempo del servidor en un cubo, establezca la relación entre el grupo de medida y la dimensión de tiempo del servidor especificando una relación en la página **Definir el uso de las dimensiones** del Asistente para cubos.  
  
### <a name="calendars"></a>Calendarios  
 En una dimensión de tiempo o una dimensión de tiempo de servidor, los atributos de periodo se agrupan en jerarquías. A estas jerarquías se las conoce normalmente como calendarios.  
  
 Las aplicaciones de Business Intelligence necesitan a menudo varias definiciones de calendarios. Por ejemplo, un departamento de recursos humanos puede realizar un seguimiento de los empleados mediante un calendario *estándar* : un calendario gregoriano de doce meses que empieza el 1 de enero y termina el 31 de diciembre. Pero el mismo departamento de recursos humanos puede hacer un seguimiento de los gastos mediante un calendario *fiscal* : un calendario de doce meses que define el año fiscal usado por la organización.  
  
 Estos calendarios pueden construirse manualmente en el Diseñador de dimensiones. Sin embargo, el Asistente para dimensiones proporciona varias plantillas de jerarquías que pueden usarse para generar automáticamente diferentes tipos de calendarios cuando se crea una dimensión de tiempo o una dimensión de tiempo de servidor. En la siguiente tabla se describen los diferentes calendarios que el Asistente para dimensiones puede generar.  
  
|Calendario|Description|  
|--------------|-----------------|  
|Calendario estándar|Calendario gregoriano de doce meses que empieza el 1 de enero y termina el 31 de diciembre.<br /><br /> Con independencia de si utiliza el Asistente para dimensiones para crear una dimensión de tiempo o una dimensión de tiempo de servidor, el asistente genera una jerarquía para un calendario estándar una vez definidos los atributos que representan los periodos de tiempo para la dimensión. Si utiliza el Asistente para dimensiones para crear una dimensión de tiempo de servidor, puede ajustar la fecha inicial del calendario estándar para que empiece otra día que no sea el 1 de enero.|  
|Calendario fiscal|Calendario fiscal de doce meses. Cuando se selecciona este calendario, deben especificarse el día y el mes de inicio del año fiscal que utilice la organización.<br /><br /> Nota: Este calendario solo está disponible si se utiliza el Asistente para dimensiones para crear una dimensión temporal del servidor.|  
|Calendario de informes (o calendario de marketing)|Calendario de informes de doce meses que incluye dos meses de cuatro semanas y un mes de cinco semanas en un patrón trimestral que se repite. Cuando se selecciona este calendario, deben especificarse el día y el mes de inicio y un patrón de repetición trimestral de 4–4–5, 4–5–4 ó 5–4–4 semanas, donde cada dígito representa el número de semanas de un mes.<br /><br /> Nota: Este calendario solo está disponible si se utiliza el Asistente para dimensiones para crear una dimensión temporal del servidor.|  
|Calendario de fabricación|Calendario que utiliza 13 periodos de cuatro semanas, divididos en tres trimestres de tres periodos y un trimestre de cuatro periodos. Cuando se selecciona este calendario, se debe especificar la semana (entre 1 y 4) y el mes de inicio del año de fabricación que utiliza la organización, así como identificar el trimestre que contiene cuatro periodos.<br /><br /> Nota: Este calendario solo está disponible si se utiliza el Asistente para dimensiones para crear una dimensión temporal del servidor.|  
|Calendario ISO 8601|Calendario estándar (8601) de Representación de fechas y horas de la Organización internacional de normalización (ISO). Este calendario tiene un número integral de semanas de siete días. El año nuevo puede empezar varios días antes o después del inicio del año nuevo según el calendario gregoriano. La primera semana de este calendario la determina la primera semana del calendario gregoriano que incluye un jueves. Por lo tanto, el primer día de esa semana, lunes, puede en realidad pertenecer al año anterior.<br /><br /> Nota: Este calendario solo está disponible si se utiliza el Asistente para dimensiones para crear una dimensión temporal del servidor.|  
  
 Cuando se crea una dimensión de tiempo de servidor y se especifican los periodos de tiempo y los calendarios que se utilizarán en esa dimensión, el Asistente para dimensiones agrega atributos a los periodos de tiempo adecuados para cada calendario especificado. Por ejemplo, si se crea una dimensión de tiempo de servidor cuyos periodos son años, e incluye dos calendarios, fiscal y de informes, el asistente agregará los atributos FiscalYear y ReportingYears, junto con el atributo Years estándar, a la dimensión. Una dimensión de tiempo de servidor también incluirá atributos para las combinaciones de periodos de tiempo seleccionados, como un atributo DayOfWeek para una dimensión que contiene días y semanas. El Asistente para dimensiones crea una jerarquía de calendarios mediante la combinación de atributos que pertenece a un solo tipo de calendario. Por ejemplo, una jerarquía de calendarios fiscales puede contener los niveles siguientes: Fiscal Year, Fiscal Half Year, Fiscal Quarter, Fiscal Month y Fiscal Day.  
  
## <a name="adding-time-intelligence-with-the-business-intelligence-wizard"></a>Agregar inteligencia de tiempo mediante el Asistente de Business Intelligence  
 Después de definir una dimensión de tiempo y agregar esa dimensión a un cubo, puede utilizar el Asistente de Business Intelligence para agregar funcionalidad de inteligencia de tiempo, como las medidas periodo hasta fecha, periodo a periodo y media rotatoria. Para obtener más información, vea [Definir cálculos de inteligencia de tiempo mediante el Asistente de Business Intelligence](../../analysis-services/multidimensional-models/define-time-intelligence-calculations-using-the-business-intelligence-wizard.md).  
  
> [!NOTE]  
>  El Asistente de Business Intelligence puede utilizarse para agregar inteligencia de tiempo a las dimensiones de tiempo de servidor. El Asistente de Business Intelligence agrega una jerarquía para admitir la inteligencia de tiempo, que debe estar vinculada a una columna de la tabla de dimensión de tiempo. Las dimensiones de tiempo de servidor no tienen una tabla de dimensión correspondiente y, por lo tanto, no pueden admitir esta jerarquía adicional.  
  
## <a name="see-also"></a>Vea también  
 [Crear una dimensión de tiempo generando una tabla de tiempos](../../analysis-services/multidimensional-models/create-a-time-dimension-by-generating-a-time-table.md)   
 [Ayuda de F1 de Asistente de Business Intelligence](http://msdn.microsoft.com/library/155ac80c-63ae-47aa-9e86-9396e3d920eb)   
 [Tipos de dimensión](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  

