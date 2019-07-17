---
title: Crear un cubo desde una plantilla sin usar una vista del origen de datos | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 28f87d9cbe6dfa0bf41a0d0547e8da7bec5659bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209099"
---
# <a name="create-a-cube-from-a-template-without-using-a-data-source-view"></a>Crear un cubo a partir de una plantilla sin usar una vista del origen de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Seleccione **Generar el cubo sin un origen de datos** en la primera página del Asistente para cubos para crear un cubo sin usar una vista del origen de datos. Posteriormente, podrá usar el Asistente para generar esquemas para generar el esquema relacional para la vista del origen de datos basándose en la estructura de cubo y, posiblemente, en otros objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para más información sobre cómo generar un esquema, vea [Asistente para generar esquemas &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/schema-generation-wizard-analysis-services.md).  
  
## <a name="selecting-the-build-method"></a>Seleccionar el método de generación  
 En la página **Seleccionar método de generación** del Asistente para cubos, haga clic en **Generar el cubo sin un origen de datos**. Para generar el cubo usando una plantilla de cubo existente, active la casilla **Usar una plantilla de cubo** . . Si prefiere no usar una plantilla, deberá establecer las opciones manualmente.  
  
 Las plantillas de cubo contienen medidas, grupos de medida, dimensiones, jerarquías y atributos predefinidos. Si selecciona una plantilla, el asistente usará las definiciones de sus objetos como base para establecer las opciones de las páginas siguientes. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se instala con varias plantillas para cubos estándar. El administrador del servidor también puede agregar plantillas de cubo o de dimensiones diseñadas específicamente para los datos de su organización.  
  
## <a name="selecting-dimensions"></a>Seleccionar dimensiones  
 Use la página **Seleccionar dimensiones** del asistente para agregar dimensiones existentes al cubo. Esta página solo aparece si ya existen dimensiones compartidas sin un origen de datos en el proyecto o en la base de datos. No muestra las dimensiones que tienen un origen de datos.  
  
 Para agregar dimensiones existentes, seleccione una o varias dimensiones en la lista **Dimensiones compartidas** y haga clic en el botón de flecha derecha ( **>** ) para moverlas a la lista **Dimensiones del cubo** . Haga clic en el botón de flecha doble ( **>>** ) si quiere mover todas las dimensiones de la lista.  
  
## <a name="defining-new-measures"></a>Definir nuevas medidas  
 Use la página **Definir nuevas medidas** del asistente para especificar las medidas y grupos de medida del nuevo cubo. Los grupos de medida que especifique aquí se corresponderán con las tablas de hechos del esquema generado. Las medidas que especifique aquí se corresponderán con las columnas numéricas sin clave de las tablas.  
  
 Si usa una plantilla para crear el cubo, las medidas de la plantilla aparecen en formato de cuadrícula debajo de **Seleccionar medidas de plantilla**. Inicialmente, aparecen seleccionadas todas las medidas. Puede desactivar la casilla situada junto a aquellas medidas que no desee incluir en el cubo. Para agregar o quitar todas las medidas de la lista, active o desactive la casilla situada en la barra de título de la cuadrícula.  
  
 Para agregar medidas al cubo, use la lista situada debajo de **Agregar nuevas medidas**. Para agregar una nueva medida, haga clic en la primera celda vacía de la columna **Nombre de medida** (donde se muestra **Agregar nueva medida**). Especifique un nombre de medida, un grupo de medida, un tipo de datos y una agregación para cada nueva medida. Para eliminar una medida de la lista **Agregar nuevas medidas** , haga clic en el icono de eliminar (**X**). Si no usa una plantilla, **Agregar nuevas medidas** es la única lista de esta página del asistente.  
  
 Las cuadrículas **Seleccionar medidas de plantilla** y **Agregar nuevas medidas** muestran valores debajo de las columnas descritas en la tabla siguiente. Puede hacer clic en un valor de cualquier lista para cambiarlo.  
  
|columna|Descripción|  
|------------|-----------------|  
|**Nombre de medida**|Cada valor de esta columna define el nombre de una medida del cubo. Haga clic en un valor de esta columna para escribir un nombre. Haga clic en **Agregar nueva medida** en esta columna para crear una nueva medida. Esta columna establece la propiedad **Name** del objeto de medida.|  
|**Grupo de medida**|El nombre del grupo de medida que contiene la medida. Haga clic en este valor para elegir o escribir un nombre. Si elimina todas las medidas que pertenecen a un grupo de medida determinado, se quita el grupo de medida. Esta columna establece la propiedad **Name** del objeto de grupo de medida.|  
|**Tipo de datos**|El tipo de datos de la medida. Haga clic en este valor para cambiar el tipo de datos. El valor predeterminado cuando se crea una medida es **Single**. Esta columna establece la propiedad **DataType** del objeto de medida.|  
|**Agregación**|La agregación estándar de la medida. Haga clic en esta celda para especificar una de las agregaciones estándar para la medida (o **Ninguna**). El valor predeterminado cuando se crea una medida es **Sum**. Esta columna establece la propiedad **AggregationFunction** del objeto de medida.|  
  
## <a name="defining-new-dimensions"></a>Definir nuevas dimensiones  
 Use la página **Definir nuevas dimensiones** del asistente para especificar las dimensiones del nuevo cubo.  
  
 Si usa una plantilla para crear el cubo, las cuadrícula situada debajo de **Seleccionar dimensiones de plantilla** mostrará las dimensiones de la plantilla. Puede desactivar la casilla situada junto a cualquier dimensión para quitarla del cubo. Para quitar todas las dimensiones de la lista, desactive la casilla situada en la barra de título de la cuadrícula. Si no usa una plantilla, la cuadrícula muestra solo la dimensión de tiempo.  
  
 Para agregar dimensiones al cubo, use la cuadrícula situada debajo de **Agregar nuevas dimensiones**. Para agregar una dimensión, haga clic en la celda de la columna **Nombre** que contiene el texto **Agregar nueva dimensión**y, a continuación, escriba un nombre para la dimensión. Para quitar una fila de la lista, haga clic en el icono de eliminar (**X**).  
  
 Las cuadrículas **Seleccionar dimensiones de plantilla** y **Agregar nuevas dimensiones** muestran valores debajo de las columnas descritas en la tabla siguiente. Puede hacer clic en un valor de cualquier lista para cambiarlo.  
  
|columna|Descripción|  
|------------|-----------------|  
|**Tipo**|Muestra el tipo de dimensión de una dimensión de la plantilla. Haga clic en esta celda para cambiar el tipo de dimensión. Esta columna establece la propiedad **Type** del objeto de dimensión.|  
|**Name**|Muestra el nombre de la dimensión. Haga clic en esta celda para escribir otro nombre. Este valor establece la propiedad **Name** del objeto de dimensión.|  
|**DVL**|Especifica que se trata de una dimensión de variación lenta (DVL). Si se activa esta casilla, se agregan los atributos Fecha de inicio de DVL, Id. original de DVL y Estado de DVL a la dimensión. La opción**DVL** aparece seleccionada de forma predeterminada si se usa una plantilla para crear el cubo y el asistente detecta estos cuatro tipos de atributos en una dimensión de plantilla.|  
|**Atributos**|Muestra los atributos que se crearán para la dimensión. Cada nombre de atributo de la lista está precedido del nombre de la dimensión. Esta lista es de solo lectura. Puede editar los atributos con el Diseñador de dimensiones una vez completado el asistente.|  
  
## <a name="defining-time-periods"></a>Definir períodos de tiempo  
 Use la página **Definir períodos de tiempo** del asistente para especificar el intervalo de fechas que desea incluir en la dimensión. Por ejemplo, puede elegir un intervalo que comience el 1 de enero del primer año de los datos y que incluya hasta unos años antes de la transacción más reciente. Las transacciones que queden fuera del intervalo no aparecerán o, si lo hacen, aparecerán como miembros desconocidos de la dimensión en función del valor de la propiedad **UnknownMemberVisible** de la dimensión. La propiedad **UnknownMemberName** especifica el título del miembro desconocido. También puede cambiar el primer día de la semana que se usará en los datos (el valor predeterminado es Domingo).  
  
> [!NOTE]  
>  La página **Definir períodos de tiempo** solo aparece si incluye una dimensión de tiempo en el cubo en la página **Definir nuevas dimensiones** del asistente.  
  
 Seleccione los períodos de tiempo (**Año**, **Semestre**, **Trimestre**, **Cuatrimestre**, **Mes**, **Diez días**, **Semana**y **Fecha**) que quiere incluir en el esquema. Es necesario que seleccione el período de tiempo Fecha. El atributo Fecha es el atributo clave de la dimensión, por lo que esta no puede funcionar sin él. También puede cambiar el idioma usado para etiquetar los miembros de la dimensión.  
  
 Los períodos de tiempo que seleccione crearán los atributos de tiempo correspondientes en la nueva dimensión de tiempo. El asistente también agrega los atributos relacionados que no aparecen en la lista. Por ejemplo, si se seleccionan los intervalos de tiempo **Año** y **Semestre** , el asistente crea los atributos Día del año, Día del semestre y Semestre del año, además de los atributos Año y Semestre.  
  
 Cuando termine de crear el cubo, podrá usar el Diseñador de dimensiones para agregar o quitar atributos de tiempo. Dado que el atributo Fecha es el atributo clave de la dimensión, no puede quitarlo. Para ocultar el atributo Fecha a los usuarios, puede cambiar la propiedad **AttributeHierarchyVisible** a **False**.  
  
 Todos los períodos de tiempo disponibles aparecen en el panel Periodos de tiempo del Diseñador de dimensiones. (Este panel reemplaza al panel **Vista del origen de datos** para las dimensiones basadas en tablas de dimensiones). Para cambiar el intervalo de fechas de una dimensión, cambie la configuración de la propiedad **Source** (enlace de tiempo) de la dimensión. Dado que se trata de un cambio estructural, deberá volver a procesar la dimensión y todos los cubos que la usan antes de examinar los datos.  
  
## <a name="specifying-additional-calendars"></a>Especificar calendarios adicionales  
 En la página **Especificar calendarios adicionales** del asistente, seleccione los calendarios en los que se basarán las jerarquías de la dimensión. Puede elegir cualquiera de los calendarios siguientes.  
  
|Calendario|Descripción|  
|--------------|-----------------|  
|Calendario fiscal|Calendario fiscal de doce meses. Si selecciona este calendario, especifique el día y el mes de inicio del año fiscal que usa la organización.|  
|Calendario de informe (o marketing)|Calendario de informes de doce meses que incluye dos meses de cuatro semanas y un mes de cinco semanas en un patrón trimestral periódico. Si selecciona este calendario, especifique el primer día y mes, el patrón de tres meses de 4-4-5, 4-5-4 o 5-4-4 semanas, donde cada dígito representa el número de semanas en un mes.|  
|Calendario de fabricación|Calendario que usa 13 períodos de cuatro semanas, divididos en tres trimestres de cuatro periodos y un trimestre de cinco períodos. Si selecciona este calendario, especifique la semana (entre 1 y 4) y el mes de inicio del año de fabricación, y el trimestre con períodos adicionales.|  
|Calendario ISO 8601|Calendario estándar (8601) de Representación de fechas y horas de la Organización internacional de normalización (ISO). Este calendario tiene un número integral de semanas de siete días. Para evitar dividir una semana, este calendario inicia un nuevo año varios días antes o después del 1 de enero.|  
  
 El calendario y la configuración que seleccione determinan los atributos que se crean en la dimensión. Por ejemplo, si selecciona los períodos de tiempo **Año** y **Trimestre** en la página **Definir períodos de tiempo** del asistente, y selecciona **Calendario fiscal** en esta página, se crearán los atributos FiscalYear, FiscalQuarter y FiscalQuarterOfYear para el calendario fiscal.  
  
 El asistente también crea jerarquías específicas para el calendario que se componen de los atributos creados para el calendario. En cada calendario, los niveles de las jerarquías se acumulan en el nivel superior. Por ejemplo, en el calendario estándar de 12 meses, el asistente crea una jerarquía de Years y Weeks o Years y Months. Sin embargo, las semanas no están contenidas de forma uniforme en los meses de un calendario estándar, por lo que no hay una jerarquía de Years, Months y Weeks. Por el contrario, las semanas de un calendario de informes o de fabricación se dividen de forma uniforme en meses, por lo que en estos calendarios las semanas se acumulan en meses.  
  
## <a name="defining-dimension-usage"></a>Definir el uso de las dimensiones  
 Use la página de **Definir el uso de las dimensiones** del asistente para especificar las medidas de cubo que agrega cada dimensión en el asistente. La cuadrícula de **Uso de dimensiones** de esta página muestra las dimensiones como filas y los grupos de medida como columnas. Active la casilla correspondiente a cualquier combinación de dimensión y grupo de medida en la que la dimensión agregue las medidas de ese grupo de medida.  
  
## <a name="completing-the-cube-wizard"></a>Completar el Asistente para cubos  
 En la página **Finalización del asistente** , revise la estructura del nuevo cubo y, en el cuadro **Nombre del cubo** , escriba un nombre para el cubo. Opcionalmente, active la casilla **Generar el esquema ahora** para iniciar el Asistente para generar esquemas. En la mayoría de los casos, no se debe activar esta casilla si piensa crear objetos adicionales. También puede usar el Diseñador de cubos para generar el esquema más adelante.  
  
  
