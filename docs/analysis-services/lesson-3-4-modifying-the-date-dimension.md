---
title: Modificar la dimensión Date | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e45dbb5f33ba17211fcb60bc6d8cca9e47aa1ee
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-3-4---modifying-the-date-dimension"></a>Lección 3-4-modificar la dimensión Date
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

En las tareas de este tema, debe crear una jerarquía definida por el usuario y cambiar los nombres de miembro que se muestran para los atributos Date, Month, Calendar Quarter y Calendar Semester. También definirá claves compuestas para los atributos, controlará el criterio de ordenación de los miembros de dimensión y definirá las relaciones de atributo.  
  
## <a name="adding-a-named-calculation"></a>Agregar un cálculo con nombre  
Puede agregar un cálculo con nombre, que es una expresión SQL representada como columna calculada en una tabla de la vista del origen de datos. Aparece la expresión y se comporta como columna en la tabla. Los cálculos con nombre permiten ampliar el esquema relacional de las tablas existentes de la vista del origen de datos sin modificar la tabla en el origen de datos subyacente. Para obtener más información, consulte [Definir cálculos con nombre en una vista del origen de datos &#40;Analysis Services&#41;](../analysis-services/multidimensional-models/define-named-calculations-in-a-data-source-view-analysis-services.md)  
  
#### <a name="to-add-a-named-calculation"></a>Para agregar un cálculo con nombre  
  
1.  Para abrir la vista del origen de datos **Adventure Works DW 2012** , haga doble clic en ella en la carpeta **Vistas del origen de datos** del Explorador de soluciones.  
  
2.  Junto a la parte inferior del panel **Tablas** , haga clic con el botón derecho en **Date**y, después, haga clic en **Nuevo cálculo con nombre**.  
  
3.  En el cuadro de diálogo **Crear cálculo con nombre** , escriba **SimpleDate** en el cuadro **Nombre de columna** y, después, escriba o copie y pegue la siguiente instrucción **DATENAME** en el cuadro **Expresión** :  
  
    ```  
    DATENAME(mm, FullDateAlternateKey) + ' ' +  
    DATENAME(dd, FullDateAlternateKey) + ', ' +  
    DATENAME(yy, FullDateAlternateKey)  
    ```  
  
    La instrucción **DATENAME** extrae los valores de año, mes y día de la columna FullDateAlternateKey. Usará esta nueva columna como el nombre mostrado para el atributo FullDateAlternateKey.  
  
4.  Haga clic en **Aceptar**y expanda **Date** en el panel **Tablas** .  
  
    Aparece el cálculo con nombre **SimpleDate** en la lista de columnas de la tabla Date, con un icono que indica que se trata de un cálculo con nombre.  
  
5.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
6.  En el panel **Tablas** , haga clic con el botón derecho en **Date**y haga clic en **Explorar datos**.  
  
7.  Desplácese hacia la derecha para revisar la última columna de la vista **Explorar la tabla Date** .  
  
    Observe que la columna **SimpleDate** aparece en la vista del origen de datos, concatenando correctamente los datos de varias columnas del origen de datos subyacente sin modificar el origen de datos original.  
  
8.  Cierre la vista **Explorar la tabla Date** .  
  
## <a name="using-the-named-calculation-for-member-names"></a>Usar el cálculo con nombre para los nombres de miembro  
Una vez que ha creado un cálculo con nombre en la vista del origen de datos, puede utilizar dicho cálculo como propiedad de un atributo.  
  
#### <a name="to-use-the-named-calculation-for-member-names"></a>Para utilizar el cálculo con nombre para los nombres de miembro  
  
1.  Abra el **Diseñador de dimensiones** para la dimensión Date en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para ello, haga doble clic en la dimensión **Date** en el nodo **Dimensiones** del **Explorador de soluciones**.  
  
2.  En el panel **Atributos** de la pestaña **Estructura de dimensión** , haga clic en el atributo **Date Key** .  
  
3.  Si la ventana Propiedades no está abierta, ábrala y, después, haga clic en el botón **Ocultar automáticamente** en la barra de título para que permanezca abierta.  
  
4.  Haga clic en el campo de la propiedad **NameColumn** situado en la parte inferior de la ventana y, después, haga clic en el botón de puntos suspensivos (**…**) para abrir el cuadro de diálogo **Columna de nombre** .  
  
5.  Seleccione **SimpleDate** al final de la lista **Columna de origen** y haga clic en **Aceptar**.  
  
6.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="creating-a-hierarchy"></a>Creación de una jerarquía  
Puede crear una nueva jerarquía si arrastra un atributo desde el panel **Atributos** hasta el panel **Jerarquías** .  
  
#### <a name="to-create-a-hierarchy"></a>Para crear una jerarquía  
  
1.  En la pestaña **Estructura de dimensión** del Diseñador de dimensiones correspondiente a la dimensión **Date** , arrastre el atributo **Calendar Year** desde el panel **Atributos** al panel **Jerarquías** .  
  
2.  Arrastre el atributo **Calendar Semester** desde el panel **Atributos** a la celda **<new level>** del panel **Jerarquías** , debajo del nivel **Calendar Year** .  
  
3.  Arrastre el atributo **Calendar Quarter** desde el panel **Atributos** a la celda **<new level>** del panel **Jerarquías** , debajo del nivel **Calendar Semester** .  
  
4.  Arrastre el atributo **English Month Name** desde el panel **Atributos** a la celda **<new level>** del panel **Jerarquías** , debajo del nivel **Calendar Quarter** .  
  
5.  Arrastre el atributo **Date Key** desde el panel **Atributos** a la celda **<new level>** del panel **Jerarquías** , debajo del nivel **English Month Name** .  
  
6.  En el panel **Jerarquías** , haga clic con el botón derecho en la barra de título de la jerarquía **Jerarquía** , haga clic en **Cambiar nombre**y escriba **Fecha del calendario**.  
  
7.  Mediante el menú contextual, en la jerarquía **Fecha del calendario** , cambie el nombre del nivel **English Month Name** a **Mes del calendario**y cambie el nombre del nivel **Date Key** a **Fecha**.  
  
8.  Elimine el atributo **Full Date Alternate Key** del panel **Atributos** , ya que no lo va a usar. Haga clic en **Aceptar** en la ventana de confirmación **Eliminar objetos** .  
  
9. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="defining-attribute-relationships"></a>Definición de relaciones de atributo  
Si los datos subyacentes lo permiten, debería definir relaciones de atributo entre atributos. La definición de relaciones de atributo acelera el procesamiento de las dimensiones, las particiones y las consultas.  
  
#### <a name="to-define-attribute-relationships"></a>Para definir relaciones de atributo  
  
1.  En el **Diseñador de dimensiones** para la dimensión **Date** , haga clic en la pestaña **Relaciones de atributo** .  
  
2.  En el diagrama, haga clic con el botón derecho en el atributo **English Month Name** y haga clic en **Nueva relación de atributo**.  
  
3.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **English Month Name**. Establezca el **Atributo relacionado** en **Calendar Quarter**.  
  
4.  En la lista **Tipo de relación**, establezca el tipo de relación en **Rígida**.  
  
    El tipo de relación es **Rígida** porque las relaciones entre los miembros no cambiarán con el tiempo.  
  
5.  Haga clic en **Aceptar**.  
  
6.  En el diagrama, haga clic con el botón derecho en el atributo **Calendar Quarter** y, después, haga clic en **Nueva relación de atributo**.  
  
7.  En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Calendar Quarter**. Establezca el **Atributo relacionado** en **Calendar Semester**.  
  
8.  En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
9. Haga clic en **Aceptar**.  
  
10. En el diagrama, haga clic con el botón derecho en el atributo **Calendar Semester** y, después, haga clic en **Nueva relación de atributo**.  
  
11. En el cuadro de diálogo **Crear relación de atributo** , el **Atributo de origen** es **Calendar Semester**. Establezca el **Atributo relacionado** en **Calendar Year**.  
  
12. En la lista **Tipo de relación** , establezca el tipo de relación en **Rígida**.  
  
13. Haga clic en **Aceptar**.  
  
14. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="providing-unique-dimension-member-names"></a>Proporcionar nombres de miembros de dimensión únicos  
En esta tarea, creará columnas con nombres descriptivos que usarán los atributos **EnglishMonthName**, **CalendarQuarter**y **CalendarSemester** .  
  
#### <a name="to-provide-unique-dimension-member-names"></a>Para proporcionar nombres de miembros de dimensión únicos  
  
1.  Para cambiar a la vista del origen de datos **[!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] DW 2012** , haga doble clic en ella en la carpeta **Vistas de origen de datos** del Explorador de soluciones.  
  
2.  En el panel **Tablas** , haga clic con el botón derecho en **Date**y, después, haga clic en **Nuevo cálculo con nombre**.  
  
3.  En el cuadro de diálogo **Crear cálculo con nombre** , escriba **MonthName** en el cuadro **Nombre de columna** y, después, escriba o copie y pegue la siguiente instrucción en el cuadro **Expresión** :  
  
    ```  
    EnglishMonthName+' '+ CONVERT(CHAR (4), CalendarYear)  
    ```  
  
    Esta instrucción concatena el mes y el año de cada mes de la tabla una nueva columna.  
  
4.  Haga clic en **Aceptar**.  
  
5.  En el panel **Tablas** , haga clic con el botón derecho en **Date**y, después, haga clic en **Nuevo cálculo con nombre**.  
  
6.  En el cuadro de diálogo **Crear cálculo con nombre** , escriba **CalendarQuarterDesc** en el cuadro **Nombre de columna** y, después, escriba o copie y pegue el siguiente script de SQL en el cuadro **Expresión** :  
  
    ```  
    'Q' + CONVERT(CHAR (1), CalendarQuarter) +' '+ 'CY ' +  
    CONVERT(CHAR (4), CalendarYear)  
    ```  
  
    Este script SQL concatena el trimestre natural y el año de cada trimestre de la tabla en una nueva columna.  
  
7.  Haga clic en **Aceptar**.  
  
8.  En el panel **Tablas** , haga clic con el botón derecho en **Date**y, después, haga clic en **Nuevo cálculo con nombre**.  
  
9. En el cuadro de diálogo **Crear cálculo con nombre** , escriba **CalendarSemesterDesc** en el cuadro **Nombre de columna** y, después, escriba o copie y pegue el siguiente script de SQL en el cuadro **Expresión** :  
  
    ```  
    CASE  
    WHEN CalendarSemester = 1 THEN 'H1' + ' ' + 'CY' + ' '   
           + CONVERT(CHAR(4), CalendarYear)  
    ELSE  
    'H2' + ' ' + 'CY' + ' ' + CONVERT(CHAR(4), CalendarYear)  
    END  
    ```  
  
    Este script SQL concatena el semestre natural y el año de cada semestre de la tabla en una nueva columna.  
  
10. Haga clic en **Aceptar.**  
  
11. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="defining-composite-keycolumns-and-setting-the-name-column"></a>Definir KeyColumns compuestas y establecer la columna de nombre  
La propiedad **KeyColumns** contiene la columna o columnas que representan la clave para el atributo. En esta tarea, definirá propiedades **KeyColumns**compuestas.  
  
#### <a name="to-define-composite-keycolumns-for-the-english-month-name-attribute"></a>Para definir KeyColumns compuestas para el atributo Spanish Month Name  
  
1.  Abra la pestaña **Estructura de dimensión** para la dimensión Date.  
  
2.  En el panel **Atributos** , haga clic en el atributo **English Month Name** .  
  
3.  En la ventana **Propiedades** , haga clic en el campo **KeyColumns** y, después, haga clic en el botón Examinar (**...**).  
  
4.  En el cuadro de diálogo **Columnas de clave** , en la lista **Columnas disponibles** , seleccione la columna **CalendarYear**y, después, haga clic en el botón **>** .  
  
5.  Las columnas **EnglishMonthName** y **CalendarYear** se muestran ahora en la lista **Columnas de clave** .  
  
6.  Haga clic en **Aceptar**.  
  
7.  Para establecer la propiedad **NameColumn** del atributo **EnglishMonthName** , haga clic en el campo **NameColumn** en la ventana Propiedades y, después, haga clic en el botón Examinar (**...**).  
  
8.  En el cuadro de diálogo **Columna de nombre** , en la lista **Columna de origen** , seleccione **MonthName**y, después, haga clic en **Aceptar**.  
  
9. En el menú **Archivo** , haga clic en **Guardar todo**.  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-quarter-attribute"></a>Para definir KeyColumns compuestas para el atributo Calendar Quarter  
  
1.  En el panel **Atributos** , haga clic en el atributo **Calendar Quarter** .  
  
2.  En la ventana **Propiedades** , haga clic en el campo **KeyColumns** y, después, haga clic en el botón Examinar (**...**).  
  
3.  En el cuadro de diálogo **Columnas de clave**, en la lista **Columnas disponibles**, seleccione la columna **CalendarYear** y, después, haga clic en el botón **>**.  
  
    Las columnas **CalendarQuarter** y **CalendarYear** se muestran ahora en la lista **Columnas de clave** .  
  
4.  Haga clic en **Aceptar**.  
  
5.  Para establecer la propiedad **NameColumn** del atributo **Calendar Quarter** , haga clic en el campo **NameColumn** en la ventana Propiedades y, después, haga clic en el botón Examinar (**...**).  
  
6.  En el cuadro de diálogo **Columna de nombre** , en la lista **Columna de origen** , seleccione **CalendarQuarterDesc**y haga clic en **Aceptar**.  
  
7.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
#### <a name="to-define-composite-keycolumns-for-the-calendar-semester-attribute"></a>Para definir KeyColumns compuestas para el atributo Calendar Semester  
  
1.  En el panel **Atributos** , haga clic en el atributo **Calendar Semester** .  
  
2.  En la ventana **Propiedades** , haga clic en el campo **KeyColumns** y, después, haga clic en el botón Examinar (**...**).  
  
3.  En el cuadro de diálogo **Columnas de clave** , en la lista **Columnas disponibles** , seleccione la columna **CalendarYear**y, después, haga clic en el botón **>** .  
  
    Las columnas **CalendarSemester** y **CalendarYear** se muestran ahora en la lista **Columnas de clave** .  
  
4.  Haga clic en **Aceptar**.  
  
5.  Para establecer la propiedad **NameColumn** del atributo **Calendar Semester** , haga clic en el campo **NameColumn** en la ventana Propiedades y, después, haga clic en el botón Examinar (**...**).  
  
6.  En el cuadro de diálogo **Columna de nombre** , en la lista **Columna de origen** , seleccione **CalendarSemesterDesc**y haga clic en **Aceptar**.  
  
7.  En el menú **Archivo** , haga clic en **Guardar todo**.  
  
## <a name="deploying-and-viewing-the-changes"></a>Implementar y ver los cambios  
Una vez que ha cambiado los atributos y las jerarquías, debe implementar los cambios y procesar de nuevo los objetos relacionados antes de ver los cambios.  
  
#### <a name="to-deploy-and-view-the-changes"></a>Para implementar y ver los cambios  
  
1.  En el menú **Generar** de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en **Implementar Tutorial de Analysis Services**.  
  
2.  Después de que aparezca el mensaje **La implementación finalizó correctamente** , haga clic en la pestaña **Explorador** del **Diseñador de dimensiones** para la dimensión **Date** y, después, haga clic en el botón Volver a conectar en la barra de herramientas del diseñador.  
  
3.  Seleccione **Calendar Quarter** en la lista **Jerarquía** . Revise los miembros de la jerarquía de atributo **Calendar Quarter** .  
  
    Observe que los nombres de los miembros de la jerarquía del atributo **Calendar Quarter** son más descriptivos y fáciles de usar porque creó un cálculo con nombre que se usa como nombre. Ahora hay miembros en la jerarquía del atributo **Calendar Quarter** para cada trimestre de cada año. Los miembros no están ordenados cronológicamente. En lugar de ello, están ordenados por trimestre y luego por año. En la siguiente tarea de este tema, modificará este comportamiento para ordenar los miembros de la jerarquía de este atributo por año y luego por trimestre.  
  
4.  Revise los miembros de las jerarquías de los atributos **English Month Name** y **Calendar Semester** .  
  
    Observe que los miembros de estas jerarquías tampoco están ordenados cronológicamente. En lugar de ello, están ordenados por mes o semestre, respectivamente, y luego por año. En la tarea siguiente de este tema, modificará este comportamiento para cambiar el criterio de ordenación.  
  
## <a name="changing-the-sort-order-by-modifying-composite-key-member-order"></a>Cambiar el criterio de ordenación modificando el orden de los miembros de clave compuesta  
En esta tarea, modificará el criterio de ordenación cambiando el orden de las claves que forman la clave compuesta.  
  
#### <a name="to-modify-the-composite-key-member-order"></a>Para modificar el orden de los miembros de clave compuesta  
  
1.  Abra la pestaña **Estructura de dimensión** del Diseñador de dimensiones para la dimensión **Date** y, después, seleccione **Calendar Semester** en el panel **Atributos** .  
  
2.  En la ventana Propiedades, revise el valor de la propiedad **OrderBy** . Dicho valor se establece en **Key**.  
  
    Los miembros de la jerarquía del atributo **Calendar Semester** están ordenados por su valor de clave. Con una clave compuesta, el orden de las claves de los miembros se basa en el primer valor de la primera clave del miembro y luego en el valor de la segunda clave del miembro. Dicho de otro modo, los miembros de la jerarquía del atributo **Calendar Semester** están ordenados primero por semestre y luego por año.  
  
3.  En la ventana Propiedades, haga clic en el botón Examinar (**...**) para cambiar el valor de la propiedad **KeyColumns** .  
  
4.  En la lista **Columnas de clave** del cuadro de diálogo **Columnas de clave** , compruebe que **CalendarSemester** está seleccionado, y, después, haga clic en la flecha abajo para invertir el orden de los miembros de esta clave compuesta. Haga clic en **Aceptar**.  
  
    Los miembros de la jerarquía de atributo ahora aparecen ordenados primero por año y luego por semestre.  
  
5.  Seleccione **Calendar Quarter** en el panel **Atributos** y, después, haga clic en el botón Examinar (**...**) de la propiedad **KeyColumns** de la ventana Propiedades.  
  
6.  En la lista **Columnas de clave** del cuadro de diálogo **Columnas de clave** , compruebe que **CalendarQuarter** está seleccionado, y, después, haga clic en la flecha abajo para invertir el orden de los miembros de esta clave compuesta. Haga clic en **Aceptar**.  
  
    Los miembros de la jerarquía de atributo ahora aparecen ordenados primero por año y luego por trimestre.  
  
7.  Seleccione **English Month Name** en el panel **Atributos** y, después, haga clic en el botón Examinar (**...**) de la propiedad **KeyColumns** de la ventana Propiedades.  
  
8.  En la lista **Columnas de clave** del cuadro de diálogo **Columnas de clave** , compruebe que **EnglishMonthName** está seleccionado, y, después, haga clic en la flecha abajo para invertir el orden de los miembros de esta clave compuesta. Haga clic en **Aceptar**.  
  
    Los miembros de la jerarquía de atributo ahora aparecen ordenados primero por año y luego por mes.  
  
9. En el menú **Generar** de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en **Implementar Tutorial de Analysis Services**. Cuando la implementación se haya completado correctamente, haga clic en la pestaña **Explorador** del Diseñador de dimensiones para la dimensión **Date** .  
  
10. En la barra de herramientas de la pestaña **Explorador** , haga clic en el botón Volver a conectar.  
  
11. Revise los miembros de las jerarquías de los atributos **Calendar Quarter** y **Calendar Semester** .  
  
    Observe que los miembros de estas jerarquías ahora están clasificados por orden cronológico, por año y luego por trimestre o semestre, respectivamente.  
  
12. Revise los miembros de la jerarquía del atributo **English Month Name** .  
  
    Observe que los miembros de la jerarquía de atributo ahora aparecen ordenados primero por año y luego alfabéticamente por mes. Esto se debe a que el tipo de datos de la columna EnglishCalendarMonth de la vista del origen de datos es una columna de cadena, basada en el tipo de datos nvarchar de la base de datos relacional subyacente. Para obtener información sobre cómo habilitar la ordenación cronológica de los meses dentro de cada año, consulte [Ordenar los miembros de atributo en función de un atributo derecho](../analysis-services/lesson-4-5-sorting-attribute-members-based-on-a-secondary-attribute.md).  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Examinar el cubo implementado](../analysis-services/lesson-3-5-browsing-the-deployed-cube.md)  
  
## <a name="see-also"></a>Vea también  
[Dimensiones en modelos multidimensionales](../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)  
  
