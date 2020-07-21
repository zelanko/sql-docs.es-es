---
title: Crear un cubo con una vista del origen de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: bec845a1-d10c-4d45-9acf-0a302adfee47
author: minewiskan
ms.author: owend
ms.openlocfilehash: 3473a760e49728ae0e91f5ab13f5346f9912ab4c
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84536652"
---
# <a name="create-a-cube-using-a-data-source-view"></a>Crear un cubo usando una vista del origen de datos
  Emplee este método para generar un nuevo cubo si piensa usar una vista del origen de datos existente. Este método le permite especificar la vista del origen de datos y seleccionar las tablas de hechos y de dimensiones que desea usar en dicha vista. A continuación, podrá elegir las dimensiones y las medidas que desea incluir en el cubo.  
  
 Para crear un cubo con un origen de datos, en el Explorador de soluciones, haga clic con el botón derecho en **Cubos** y seleccione **Nuevo cubo**. Se abrirá el Asistente para cubos.  
  
## <a name="selecting-the-build-method"></a>Seleccionar el método de generación  
 En la página **Seleccionar método de generación** del asistente, haga clic en **Generar el cubo con un origen de datos**.  
  
 Si activa la casilla de **Generación automática** , el asistente analiza la vista del origen de datos para configurar el cubo y sus dimensiones automáticamente. El asistente identifica las tablas de hechos y de dimensiones, selecciona las medidas que se van a incluir en el cubo y genera las jerarquías. En cada una de sus páginas tendrá la oportunidad de examinar y cambiar las decisiones tomadas al seleccionar **Generación automática** . Si no selecciona **Generación automática**, deberá tomar estas decisiones manualmente.  
  
 Si selecciona **Generación automática**, puede hacer clic **Finalizar** en cualquier página del asistente para saltar a la última página y aceptar las configuraciones predeterminadas para las páginas restantes del asistente. En la última página del asistente, puede revisar la estructura del cubo antes de finalizar el asistente.  
  
 Si no selecciona **Generación automática**, deberá seleccionar manualmente las tablas de hechos y de dimensiones. El asistente generará todas las dimensiones que le indique, pero deberá usar el Diseñador de dimensiones para generar manualmente jerarquías definidas por el usuario en las dimensiones. Es posible que este requisito no le afecte si ya ha creado las dimensiones que desea usar en el cubo antes de ejecutar el Asistente para cubos.  
  
## <a name="selecting-the-data-source-view"></a>Seleccionar la vista del origen de datos  
 Si usa un origen de datos existente para crear un cubo, el primer paso es especificar la vista del origen de datos en la que se basará el cubo. En la página **Seleccionar vista del origen de datos** del asistente, seleccione una vista del origen de datos existente. En el panel de vista previa, puede ver las tablas de una vista del origen de datos seleccionada. Para mostrar el esquema de una vista del origen de datos seleccionada, haga clic **Examinar**.  
  
 Si la vista del origen de datos que desea usar no aparece, en el Asistente para cubos, haga clic en **Cancelar**y abra el Asistente para vistas del origen de datos. También puede hacer clic en **Agregar nuevo elemento** en el menú **Archivo** para agregar una vista del origen de datos existente de otra base de datos (u otra ubicación). Para más información sobre cómo crear vistas del origen de datos, vea [Vistas del origen de datos en modelos multidimensionales](data-source-views-in-multidimensional-models.md).  
  
> [!NOTE]  
>  Una vista del origen de datos debe contener al menos una tabla que se mostrará en esta página. No puede crear un cubo basado en una vista del origen de datos que no contiene ninguna tabla.  
  
## <a name="identify-fact-and-dimension-tables"></a>Identificar tablas de hechos y de dimensiones  
 En el Asistente para cubos, use la página **Identificar tablas de hechos y de dimensiones** del asistente para seleccionar las tablas de hechos y de dimensiones necesarias para crear el cubo. Si ha seleccionado la casilla de **Generación automática** para crear el cubo, las tablas de hechos o de dimensiones que detecte el asistente estarán seleccionadas cuando aparezca por primera vez esta página. Si el asistente detecta una tabla que es al mismo tiempo una tabla de hechos y una tabla de dimensiones, ambas columnas estarán seleccionadas. Si el asistente detecta una tabla que no es ninguna de ellas, no se seleccionará ninguna columna. Si no necesita una tabla para el diseño del cubo, desactive las casillas **Hechos** y **Dimensiones** .  
  
 Si no activó la casilla **Generación automática** , deberá realizar todas las selecciones manualmente. Use la pestaña **Tablas** o la pestaña **Diagrama** :  
  
-   La pestaña **Tablas** muestra las tablas en formato de tabla. Active la casilla de la columna **Hechos** o de la columna **Diagrama** .  
  
-   La pestaña **Diagrama** muestra el esquema de vista del origen de datos. Las tablas están codificadas mediante colores para indicar hechos o dimensiones. Haga clic en cualquier tabla del esquema y, a continuación, haga clic en **Hechos** o **Dimensiones** para seleccionar o borrar el valor de esa tabla. Para cambiar la ampliación, use el botón **Zoom** .  
  
> [!NOTE]  
>   En la pestaña **Diagrama** , puede ampliar o maximizar la ventana del asistente para ver el esquema.  
  
 Si hay un tabla de dimensiones de tiempo en la vista del origen de datos, selecciónela en la lista **Tabla de dimensiones de tiempo** . Si no hay ninguno, deje **\<None>** seleccionado. Este es el elemento predeterminado en la lista. Cuando se selecciona una tabla como la tabla de dimensiones de tiempo, también se la selecciona como tabla de dimensiones en las pestañas **Tablas** y **Diagrama** .  
  
## <a name="defining-time-periods"></a>Definir períodos de tiempo  
 Si especificó una tabla de dimensiones de tiempo al seleccionar tipos de tabla, use la página **Definir períodos de tiempo** del asistente para especificar las columnas de la tabla que se corresponden con períodos estándar. Busque los períodos estándar en **Nombre de la propiedad de tiempo**. Para cada fila que tenga una columna correspondiente en la tabla de dimensiones de tiempo, elija la columna correcta en **Columnas de la tabla de tiempos**. El asistente usa las asociaciones especificadas para crear atributos y sugerir jerarquías de tiempo que tengan sentido para los datos. Estas asociaciones también establecen la propiedad **Tipo** para los atributos correspondientes de la nueva dimensión de tiempo. El asistente crea entonces una dimensión de tiempo basada en una tabla de dimensiones de tiempo.  
  
 Una vez creado el cubo, puede usar el Asistente de Business Intelligence para agregar mejoras de inteligencia de tiempo al cubo. Estas mejoras incluyen vistas de período hasta fecha, media rotatoria y período hasta período.  
  
## <a name="selecting-dimensions"></a>Seleccionar dimensiones  
 Use la página **Seleccionar dimensiones** del asistente para agregar dimensiones existentes al cubo. Esta página solo aparece si ya hay dimensiones compartidas que corresponden a tablas de dimensiones del cubo nuevo.  
  
 Para agregar dimensiones existentes, selecciónelas en la lista **Dimensiones compartidas** y haga clic en el botón de flecha derecha (**>**) para moverlas a la lista **Dimensiones del cubo** . Haga clic en el botón de flecha doble ( **>>** ) para desplace todas las dimensiones de la lista.  
  
 Si una dimensión existente no aparece en la lista y cree que debería hacerlo, puede hacer clic en **Atrás** y cambiar la configuración del tipo de tabla para una o varias tablas. Asimismo, una dimensión existente debe estar relacionada con al menos una de las tablas de hechos del cubo que aparecen en la lista **Dimensiones compartidas** .  
  
## <a name="selecting-measures"></a>Seleccionar medidas  
 Use la página **Seleccionar medidas** del asistente para seleccionar las medidas que desea incluir en el cubo. Cada tabla marcada como tabla de hechos aparece como un grupo de medida en esta lista, y cada columna numérica sin clave aparece como una medida en la lista. De forma predeterminada, se seleccionan todas las medidas de todos los grupos de medida. Puede desactivar la casilla situada junto a las medidas que no desea incluir en el cubo. Para quitar todas las medidas de un grupo de medida del cubo, desactive la casilla **Grupos de medida y medidas** .  
  
 Los nombres de las medidas que aparecen en **Grupos de medida y medidas** reflejan nombres de columna. Puede hacer clic en la celda que contiene un nombre para modificarlo.  
  
 Para ver los datos de cualquier medida, haga clic con el botón derecho en una de las filas de medida de la lista y haga clic en **Ver datos de muestra**. Se abrirá el **Visor de muestras de datos** , que mostrará hasta los primeros 1.000 registros de la tabla de hechos correspondiente.  
  
## <a name="reviewing-new-dimensions"></a>Revisar las nuevas dimensiones  
 Use la página **Revisar las nuevas dimensiones** del asistente para revisar las estructuras de las dimensiones creadas por el asistente. Las dimensiones se muestran en esta página del asistente en la vista de árbol **Nuevas dimensiones** . Puede revisar las dimensiones de varias maneras:  
  
-   Expanda cualquier dimensión para ver sus atributos y jerarquías.  
  
-   Expanda la carpeta **Atributos** en cualquier dimensión para ver sus atributos.  
  
-   Expanda la carpeta **Jerarquía** en cualquier dimensión para ver sus jerarquías.  
  
-   Expanda cualquier jerarquía para ver sus niveles.  
  
> [!NOTE]  
>  Puede ampliar o maximizar la ventana del asistente para ver mejor el árbol.  
  
 Para quitar cualquier objeto del árbol del cubo, desactive la casilla situada junto a él. Si se desactiva la casilla situada junto a un objeto, también se quitan todos los objetos que aparecen debajo de él. Las dependencias entre objetos se aplican, por lo que, si quita un atributo, los niveles de jerarquía que dependen de este también se quitan. Por ejemplo, si se desactiva una casilla situada junto a una jerarquía, se desactivarán las casillas situadas junto a todos los niveles de la jerarquía y se quitarán los niveles, así como las jerarquías. El atributo clave de una dimensión no se puede quitar.  
  
 Para cambiar el nombre de cualquier dimensión, atributo, jerarquía o nivel, haga clic en el nombre o haga clic con el botón secundario en el nombre y, a continuación, en el menú contextual, haga clic en cambiar **nombre \<object> **, donde **\<object>** es **dimensión**, **atributo**o **nivel**.  
  
 No hay necesariamente una relación uno a uno entre el número de tablas de dimensiones definidas en la página **Identificar tablas de hechos y de dimensiones** del asistente y el número de dimensiones incluidas en esta página del asistente. Dependiendo de las relaciones entre las tablas de la vista del origen de datos, el asistente puede usar dos o más tablas para generar una dimensión (por ejemplo, tal y como requiere un esquema de copo de nieve).  
  
## <a name="completing-the-cube-wizard"></a>Completar el Asistente para cubos  
 En la página **Finalización del asistente** , puede ver los grupos de medida, las medidas y las dimensiones del nuevo cubo. En el cuadro **Nombre del cubo** , escriba un nombre para el cubo. A continuación, si está satisfecho con el cubo, haga clic en **Finalizar**. Haga clic en **Atrás** si desea volver a cualquier página anterior del asistente y realizar cambios.  
  
  
