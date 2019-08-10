---
title: Agregar una vista del origen de datos para datos del centro de llamadas (tutorial intermedio de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a448e7e4-dbd1-4d31-90bc-4d4a1c23b352
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 04f930c42b0e41a9f10b35d10295a38e8dac7490
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68888685"
---
# <a name="adding-a-data-source-view-for-call-center-data-intermediate-data-mining-tutorial"></a>Agregar una vista del origen de datos para datos del centro de llamadas (Tutorial intermedio de minería de datos)
  En esta tarea, agregará una vista del origen de datos que se usará para tener acceso a los datos del centro de llamadas. Se usarán los mismos datos para crear tanto el modelo de red neuronal inicial para la exploración como el modelo de regresión logístico que se empleará para hacer las recomendaciones.  
  
 También usará el Diseñador de vistas del origen de datos para agregar una columna para el día de la semana. Esto se debe a que, aunque los datos de origen hacen el seguimiento de los datos del centro de llamadas de por fechas, su experiencia indica que hay patrones que se repiten en términos de volumen de llamadas y calidad del servicio, dependiendo de si el día es un fin de semana o un día de la semana.  
  
## <a name="procedures"></a>Procedimientos  
  
#### <a name="to-add-a-data-source-view"></a>Para agregar una vista del origen de datos  
  
1.  En **Explorador de soluciones**, haga clic con el botón secundario en **vistas del origen de datos**y seleccione **nueva vista del origen de datos**.  
  
     Se abrirá el Asistente para vistas del origen de datos.  
  
2.  En la página **Asistente para vistas del origen de datos** , haga clic en **Siguiente**.  
  
3.  En la página **seleccionar un origen de datos** , en **orígenes de datos relacionales**, seleccione el origen de [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] datos. Si no tiene este origen de datos, vea [tutorial básico de minería de datos](../../2014/tutorials/basic-data-mining-tutorial.md). Haga clic en **Next**.  
  
4.  En la página **seleccionar tablas y vistas** , seleccione la tabla siguiente y, a continuación, haga clic en la flecha derecha para agregarla a la vista del origen de datos:  
  
    -   **FactCallCenter (dbo)**  
  
    -   **DimDate**  
  
5.  Haga clic en **Next**.  
  
6.  En la página **finalización del asistente** , la vista del origen de datos se [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]denomina de forma predeterminada. Cambie el nombre a **callcenter**y, a continuación, haga clic en **Finalizar**.  
  
     Se abre el diseñador de vistas del origen de datos para mostrar la vista del origen de datos **callcenter** .  
  
7.  Haga clic con el botón secundario en el panel vista del origen de datos y seleccione **Agregar o quitar tablas**. Seleccione la tabla **DimDate** y haga clic en **Aceptar**.  
  
     Una relación debe agregarse automáticamente entre las `DateKey` columnas de cada tabla. Usará esta relación para obtener la columna **EnglishDayNameOfWeek**de la tabla **DimDate** y usarla en el modelo.  
  
8.  En el diseñador de vistas del origen de datos, haga clic con el botón secundario en la tabla **FactCallCenter**y seleccione **nuevo cálculo con nombre**.  
  
     En el cuadro de diálogo **crear cálculo con nombre** , escriba los valores siguientes:  
  
    |||  
    |-|-|  
    |**Nombre de columna**|DayOfWeek|  
    |**Descripción**|Obtiene el día de la semana en la tabla DimDate|  
    |**Expresión**|`(SELECT EnglishDayNameOfWeek AS DayOfWeek FROM DimDate where FactCallCenter.DateKey = DimDate.DateKey)`|  
  
     Para comprobar que la expresión crea los datos que necesita, haga clic con el botón secundario en la tabla **FactCallCenter**y, a continuación, seleccione **explorar datos**.  
  
9. Dedique un minuto a revisar los datos disponibles, para entender cómo se usan en la minería de datos:  
  
|Nombre de columna|Contiene|  
|-----------------|--------------|  
|FactCallCenterID|Una clave arbitraria que se creó cuando se importaron los datos al almacenamiento de datos.<br /><br /> Esta columna identifica los registros únicos y debe usarse como clave de caso para el modelo de minería de datos.|  
|DateKey|La fecha de la operación en el centro de llamadas, expresada como un entero. Las claves de fecha se usan a menudo en los almacenamientos de datos, pero puede que desee obtener la fecha con formato de fecha y hora si va a agrupar los valores por fecha.<br /><br /> Observe que las fechas no son únicas, ya que el proveedor facilita un informe independiente para cada turno de cada día de trabajo.|  
|WageType|Indica si el día era un día de la semana, un fin de semana o un día festivo.<br /><br /> Es posible que haya una diferencia en la calidad del servicio de atención al cliente en los fines de semana y los días de la semana, por lo que usará esta columna como una entrada.|  
|Shift|Indica el turno para el que se registran las llamadas. Este centro de llamadas divide el día laborable en cuatro turnos: AM, PM1, PM2 y medianoche.<br /><br /> Es posible que el turno afecte a la calidad del servicio al cliente; por eso usará esto como entrada.|  
|LevelOneOperators|Indica el número de operadores de nivel 1 en el arancel.<br /><br /> Los empleados de centro de llamadas comienzan en el nivel 1, de modo que estos empleados tienen menos experiencia.|  
|LevelTwoOperators|Indica el número de operadores de nivel 2 en servicio.<br /><br /> Un empleado debe registrar un número determinado de horas de servicio para calificar como operador de nivel 2.|  
|TotalOperators|Número total de operadores presentes durante el turno.|  
|Calls|Número de llamadas recibidas durante el turno.|  
|AutomaticResponses|Número de llamadas procesadas por completo de forma automática (sistema de respuesta de voz interactiva o IVR).|  
|Orders|Número de pedidos resultantes de las llamadas.|  
|IssuesRaised|Número de incidencias que requieren seguimiento y que se generaron a través de llamadas.|  
|AverageTimePerIssue|Promedio de tiempo que se tarda en atender una llamada entrante.|  
|ServiceGrade|Una métrica que indica la calidad de servicio general, medida como la *tasa* de abandono para todo el turno. Cuanto más alta es la tasa de abandono, más probabilidades hay de que los clientes no estén satisfechos y de que se pierdan posibles pedidos.|  
  
 Tenga en cuenta que los datos incluyen cuatro columnas diferentes basadas en una sola columna de fecha `WageType`:, DayOfWeek `Shift`, y `DateKey`. Normalmente en la minería de datos no es aconsejable usar varias columnas derivadas de los mismos datos, ya que los valores están demasiado correlacionados entre sí y pueden ocultar otros patrones.  
  
 Sin embargo, no usaremos `DateKey` en el modelo porque contiene demasiados valores únicos. No hay ninguna relación directa entre `Shift` y `WageType` DayOfWeek, y y **DayOfWeek** solo se relacionan parcialmente. Si le preocupa que los datos sean colineales, podría crear la estructura con todas las columnas disponibles y, a continuación, omitir varias columnas en cada modelo y probar el efecto.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear un tutorial de minería de datos &#40;intermedio de modelo y estructura de red neuronal&#41;](../../2014/tutorials/creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)  
  
  
