---
title: Agregar datos de una vista de datos del centro de llamadas (Tutorial de minería de datos intermedio) del origen | Documentos de Microsoft
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a448e7e4-dbd1-4d31-90bc-4d4a1c23b352
caps.latest.revision: 18
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 128ff8a4cbd1bafcf9c15c32f5cd7c5e127710d9
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312333"
---
# <a name="adding-a-data-source-view-for-call-center-data-intermediate-data-mining-tutorial"></a>Agregar una vista del origen de datos para datos del centro de llamadas (Tutorial intermedio de minería de datos)
  En esta tarea, agregará una vista del origen de datos que se usará para tener acceso a los datos del centro de llamadas. Se usarán los mismos datos para crear tanto el modelo de red neuronal inicial para la exploración como el modelo de regresión logístico que se empleará para hacer las recomendaciones.  
  
 También usará el Diseñador de vistas del origen de datos para agregar una columna para el día de la semana. Esto se debe a que, aunque los datos de origen hacen el seguimiento de los datos del centro de llamadas de por fechas, su experiencia indica que hay patrones que se repiten en términos de volumen de llamadas y calidad del servicio, dependiendo de si el día es un fin de semana o un día de la semana.  
  
## <a name="procedures"></a>Procedimientos  
  
#### <a name="to-add-a-data-source-view"></a>Para agregar una vista del origen de datos  
  
1.  En **el Explorador de soluciones**, haga clic en **vistas del origen de datos**y seleccione **nueva vista del origen de datos**.  
  
     Se abrirá el Asistente para vistas del origen de datos.  
  
2.  En la página **Asistente para vistas del origen de datos** , haga clic en **Siguiente**.  
  
3.  En el **seleccionar un origen de datos** página, en **orígenes de datos relacionales**, seleccione el [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] origen de datos. Si no tiene este origen de datos, vea [Tutorial básico de minería de datos](../../2014/tutorials/basic-data-mining-tutorial.md). Haga clic en **Siguiente**.  
  
4.  En el **seleccionar tablas y vistas** , seleccione la tabla siguiente y, a continuación, haga clic en la flecha derecha para agregarlo a la vista del origen de datos:  
  
    -   **FactCallCenter (dbo)**  
  
    -   **DimDate**  
  
5.  Haga clic en **Siguiente**.  
  
6.  En el **finalización del Asistente para** página, de forma predeterminada la vista del origen de datos se denomina [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]. Cambie el nombre a **CallCenter**y, a continuación, haga clic en **finalizar**.  
  
     Se abre el Diseñador de vistas del origen de datos para mostrar el **CallCenter** vista del origen de datos.  
  
7.  Haga clic en el panel de vista del origen de datos y seleccione **agregar o quitar tablas**. Seleccione la tabla, **DimDate** y haga clic en **Aceptar**.  
  
     Se debe agregar automáticamente una relación entre el `DateKey` columnas de cada tabla. Utilizará esta relación para obtener la columna **EnglishDayNameOfWeek**, desde el **DimDate** tabla y utilizarla en el modelo.  
  
8.  En el Diseñador de vistas de origen de datos, haga clic en la tabla, **FactCallCenter**y seleccione **nuevo cálculo con nombre**.  
  
     En el **crear cálculo con nombre** diálogo cuadro, escriba los siguientes valores:  
  
    |||  
    |-|-|  
    |**Nombre de columna**|DayOfWeek|  
    |**Descripción**|Obtiene el día de la semana en la tabla DimDate|  
    |**Expresión**|`(SELECT EnglishDayNameOfWeek AS DayOfWeek FROM DimDate where FactCallCenter.DateKey = DimDate.DateKey)`|  
  
     Para comprobar que la expresión crea los datos necesita, haga clic en la tabla **FactCallCenter**y, a continuación, seleccione **explorar datos**.  
  
9. Dedique un minuto a revisar los datos disponibles, para entender cómo se usan en la minería de datos:  
  
|Nombre de columna|Contiene|  
|-----------------|--------------|  
|FactCallCenterID|Una clave arbitraria que se creó cuando se importaron los datos al almacenamiento de datos.<br /><br /> Esta columna identifica los registros únicos y debe usarse como clave de caso para el modelo de minería de datos.|  
|DateKey|La fecha de la operación en el centro de llamadas, expresada como un entero. Las claves de fecha se usan a menudo en los almacenamientos de datos, pero puede que desee obtener la fecha con formato de fecha y hora si va a agrupar los valores por fecha.<br /><br /> Observe que las fechas no son únicas, ya que el proveedor facilita un informe independiente para cada turno de cada día de trabajo.|  
|WageType|Indica si el día es un día de la semana, un fin de semana o un día no laborable.<br /><br /> Es posible que haya una diferencia en la calidad del servicio al cliente los fines de semana frente a los días laborables por lo que usará esta columna como entrada.|  
|Shift|Indica el turno para el que se registran las llamadas. Este centro de llamadas divide su jornada laboral en cuatro turnos: uno por la mañana (AM), dos por la tarde (PM1 y PM2) y uno por la noche (Midnight).<br /><br /> Es posible que el turno afecte a la calidad del servicio al cliente; por eso usará esto como entrada.|  
|LevelOneOperators|Indica el número de operadores de nivel 1 del servicio.<br /><br /> Los empleados de centro de llamadas comienzan en el nivel 1, de modo que estos empleados tienen menos experiencia.|  
|LevelTwoOperators|Indica el número de operadores de nivel 2 en servicio.<br /><br /> Un empleado debe llevar un número determinado de horas de servicio para ser calificadas como un operador de nivel 2.|  
|TotalOperators|Número total de operadores presentes durante el turno.|  
|Calls|Número de llamadas recibidas durante el turno.|  
|AutomaticResponses|Número de llamadas procesadas por completo de forma automática (sistema de respuesta de voz interactiva o IVR).|  
|Orders|Número de pedidos resultantes de las llamadas.|  
|IssuesRaised|Número de incidencias que requieren seguimiento y que se generaron a través de llamadas.|  
|AverageTimePerIssue|Promedio de tiempo que se tarda en atender una llamada entrante.|  
|ServiceGrade|Una medida que indica la calidad general del servicio, se mide como el *tasa de abandono* del turno completo. Cuanto más alta es la tasa de abandono, más probabilidades hay de que los clientes no estén satisfechos y de que se pierdan posibles pedidos.|  
  
 Tenga en cuenta que los datos contienen cuatro columnas diferentes que se basan en una sola columna de fecha: `WageType`, **DayOfWeek**, `Shift`, y `DateKey`. Normalmente en la minería de datos no es aconsejable usar varias columnas derivadas de los mismos datos, ya que los valores están demasiado correlacionados entre sí y pueden ocultar otros patrones.  
  
 Sin embargo, Microsoft no usará `DateKey` en el modelo porque contiene demasiados valores únicos. No hay ninguna relación directa entre `Shift` y **DayOfWeek**, y `WageType` y **DayOfWeek** solo están parcialmente relacionados. Si le preocupa que los datos sean colineales, podría crear la estructura con todas las columnas disponibles y, a continuación, omitir varias columnas en cada modelo y probar el efecto.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear una estructura de red neuronal y el modelo &#40;intermedio de Tutorial de minería de datos&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  