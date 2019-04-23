---
title: Interfaz de usuario del Diseñador de consultas relacionales (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10012"
helpviewer_keywords:
- query designers
- accessing data, query designer
- relational query designer
ms.assetid: cd5fa70c-5218-40d5-9ae6-02d798b5c485
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: efd8e80d223e75503bd034c77483d60a51ff9e1a
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59947701"
---
# <a name="relational-query-designer-user-interface-report-builder"></a>Interfaz de usuario del Diseñador de consultas relacionales (Generador de informes)
  El generador de informes proporciona un diseñador gráfico de consultas y un diseñador de consultas basado en texto para ayudarle a crear una consulta que especifique los datos deben recuperarse [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)] bases de datos relacionales y [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] para un conjunto de datos. Use el diseñador gráfico de consultas para explorar los metadatos, crear una consulta de forma interactiva y ver los resultados de la consulta. Use el diseñador de consultas basado en texto para ver la consulta creada por el diseñador gráfico de consultas o para modificar una consulta. También puede importar una consulta existente de un archivo o informe.  
  
> [!NOTE]  
>  En el Generador de informes, para especificar una consulta para los tipos de orígenes de datos Oracle, OLE DB, ODBC y Teradata, debe usarse el diseñador de consultas basado en texto. Para más información, vea [Interfaz de usuario del Diseñador de consultas basado en texto &#40;Generador de informes&#41;](text-based-query-designer-user-interface-report-builder.md).  
  
> [!IMPORTANT]  
>  Los usuarios tienen acceso a los orígenes de datos cuando crean y ejecutan las consultas. Debe conceder permisos mínimos para los orígenes de datos, por ejemplo permisos de solo lectura.  
  
## <a name="graphical-query-designer"></a>Diseñador gráfico de consultas  
 En el diseñador gráfico de consultas, puede explorar las tablas y vistas de base de datos, y construir de forma interactiva la instrucción SQL SELECT que especifica las tablas y columnas de base de datos de las que se van a recuperar los datos para un conjunto de datos. Debe elegir los campos que se incluirán en el conjunto de datos y, si lo desea, especificar los filtros que limitan los datos en el conjunto de datos. Puede especificar que los filtros se usan como parámetros y proporcionar el valor del filtro en tiempo de ejecución. Si elige varias tablas relacionadas, el diseñador de consultas describe la relación entre conjuntos de dos.  
  
 El diseñador gráfico de consultas se divide en tres áreas. El diseño del diseñador de consultas cambia en función de si la consulta usa tablas o vistas, o bien funciones con valores de tabla o procedimientos almacenados.  
  
> [!NOTE]  
>  [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] no admite procedimientos almacenados o funciones con valores de tabla.  
  
 La figura siguiente muestra el diseñador gráfico de consultas cuando se utiliza con tablas o vistas.  
  
 ![Diseñador gráfico de consultas](../../analysis-services/media/rsqd-relational-graphical.gif "Diseñador gráfico de consultas")  
  
 La figura siguiente muestra el diseñador gráfico de consultas cuando se utiliza con funciones con valores de tabla o procedimientos almacenados.  
  
 ![Procedimiento almacenado en un diseñador gráfico de consultas](../../analysis-services/media/rs-relational-graphical-sp.gif "Procedimiento almacenado en un diseñador gráfico de consultas")  
  
 En la siguiente tabla se describe la función de cada panel.  
  
 [Vista de base de datos](#DatabaseView)  
 Muestra una vista jerárquica de tablas, vistas, procedimientos almacenados y funciones con valores de tabla organizados por esquema de la base de datos.  
  
 [Campos seleccionados](#SelectedFields)  
 Muestra la lista de nombres de campo de base de datos de los elementos seleccionados en el panel Vista de base de datos. Estos campos se convierten en la colección de campos para el conjunto de datos de informe.  
  
 [Parámetros de función](#FunctionParameters)  
 Muestra la lista de parámetros de entrada para procedimientos almacenados o funciones con valores de tabla en el panel Vista de base de datos.  
  
 [Relaciones](#Relationships)  
 Muestra una lista de relaciones que se infieren de los campos seleccionados para tablas o vistas en el panel Vista de base de datos o las relaciones que creó manualmente.  
  
 [Filtros aplicados.](#AppliedFilters)  
 Muestra una lista de campos y criterios de filtro para tablas o vistas en la Vista de base de datos.  
  
 [Resultados de la consulta](#QueryResults)  
 Muestra datos de ejemplo para el conjunto de resultados de la consulta generada automáticamente.  
  
###  <a name="DatabaseView"></a> Panel Vista de base de datos  
 El panel Vista de base de datos muestra los metadatos de los objetos de base de datos que el usuario tiene permiso para ver, que se determinan mediante la conexión a un origen de datos y las credenciales. La vista jerárquica muestra objetos de base de datos organizados por esquema de la base de datos. Expanda el nodo de cada esquema para ver las tablas, vistas, procedimientos almacenados y funciones con valores de tabla. Expanda una tabla o vista para ver las columnas.  
  
###  <a name="SelectedFields"></a> Panel Campos seleccionados  
 El panel Campos seleccionados muestra los campos en el conjunto de datos de informe y los grupos y agregados para incluir en la consulta.  
  
 Se muestran las siguientes opciones:  
  
-   **Campos seleccionados** : muestra los campos de base de datos seleccionados para tablas o vistas, o los parámetros de entrada para procedimientos almacenados o funciones con valores de tabla. Los campos que se muestran en este panel se convierten en la colección de campos para el conjunto de datos de informe.  
  
     Utilice el panel Datos de informe para mostrar la colección de campos para un conjunto de datos de informe. Estos campos representan los datos que pueden mostrarse en tablas, gráficos y otros elementos de informe al visualizar un informe.  
  
-   **Grupo y agregado** : alterna el uso de la agrupación y los agregados en la consulta. Si desactiva la característica de agrupación y agregados después de agregar agrupaciones y agregados, estos se quitan. El texto **(ninguno)** indica que no se usa ninguna agrupación ni agregados. Si activa de nuevo la característica de agrupación y agregados, se restauran las agrupaciones y agregados anteriores.  
  
-   **Eliminar campo** : elimina el campo seleccionado.  
  
#### <a name="group-and-aggregate"></a>Grupo y agregado  
 Las consultas a las bases de datos con una tabla grande podrían devolver un número de filas de datos que sea demasiado elevado para ser útil y afecte al rendimiento en la red que transporta la ingente cantidad de datos y en el servidor de informes que procesa el informe. Para limitar el número de filas de datos, la consulta puede incluir agregados de SQL que resumen los datos en el servidor de bases de datos. Los agregados de SQL son diferentes de los agregados del lado cliente, que se aplican cuando se representa el informe.  
  
 Los agregados proporcionan resúmenes de datos y los datos se agrupan para admitir el agregado que ofrece los datos de resumen. Al utilizar un agregado en la consulta, los otros campos que devuelve se agrupan automáticamente y la consulta incluye la cláusula de SQL GROUP BY. Puede resumir los datos sin agregar un agregado utilizando solo la opción **Agrupar por** en la lista **Grupo y agregado** . Muchos de los agregados incluyen una versión que utiliza la palabra clave DISTINCT. Al incluir DISTINCT, se eliminan los valores duplicados.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa [!INCLUDE[tsql](../../../includes/tsql-md.md)] y de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] usa [!INCLUDE[DWsql](../../includes/dwsql-md.md)]. Ambos dialectos del lenguaje SQL admiten la cláusula, la palabra clave y los agregados que el diseñador de consultas proporciona.  
  
 Para más información sobre [!INCLUDE[tsql](../../../includes/tsql-md.md)], vea [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference) en los [Libros en pantalla](https://go.microsoft.com/fwlink/?LinkId=141687) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en msdn.microsoft.com.  
  
 En la siguiente tabla se enumeran los agregados y se proporciona una breve descripción de los mismos.  
  
|Agregado|Descripción|  
|---------------|-----------------|  
|Avg|Devuelve el promedio de los valores de un grupo. Implementa el agregado AVG de SQL.|  
|Count|Devuelve el número de elementos de un grupo. Implementa el agregado COUNT de SQL.|  
|Count Big|Devuelve el número de elementos de un grupo. Es el agregado de SQL COUNT_BIG. La diferencia entre COUN y COUNT_BIG es que COUNT_BIG siempre devuelve un valor de tipo de datos `bigint`.|  
|Min|Devuelve el valor mínimo en un grupo. Implementa el agregado de SQL MIN.|  
|Max|Devuelve el valor máximo en un grupo. Implementa el agregado de SQL MAX.|  
|StDev|Devuelve la desviación estadística estándar de todos los valores de un grupo. Implementa el agregado de SQL STDEV.|  
|StDevP|Devuelve la desviación estadística estándar para la población de todos los valores de una expresión especificada de grupo. Implementa el agregado de SQL STDEVP.|  
|Sum|Devuelve la suma de todos los valores de un grupo. Implementa el agregado de SQL SUM.|  
|Var|Devuelve la varianza estadística de todos los valores del grupo. Implementa el agregado de SQL VAR.|  
|VarP|Devuelve la varianza estadística de la población de todos los valores del grupo. Implementa el agregado de SQL VARP.|  
|Avg Distinct|Devuelve los promedios únicos. Implementa una combinación de la agregación AVG y la palabra clave DISTINCT.|  
|Count Distinct|Devuelve recuentos únicos. Implementa una combinación del agregado COUNT y la palabra clave DISTINCT.|  
|Count Big Distinct|Devuelve el recuento único de los elementos de un grupo. Implementa una combinación del agregado COUNT_BIG y la palabra clave DISTINCT.|  
|StDev Distinct|Devuelve las desviaciones estándar estadísticas únicas. Implementa una combinación del agregado STDEV y la palabra clave DISTINCT.|  
|StDevP Distinct|Devuelve las desviaciones estándar estadísticas únicas. Implementa una combinación del agregado STDEVP y la palabra clave DISTINCT.|  
|Sum Distinct|Devuelve sumas únicas. Implementa una combinación del agregado SUM y la palabra clave DISTINCT.|  
|Var Distinct|Devuelve varianzas estadísticas únicas. Implementa una combinación del agregado VAR y la palabra clave DISTINCT.|  
|VarP Distinct|Devuelve varianzas estadísticas únicas. Implementa una combinación del agregado VARP y la palabra clave DISTINCT.|  
  
###  <a name="FunctionParameters"></a> Panel Parámetros de función  
 El panel Parámetros de función muestra los parámetros para un procedimiento almacenado o función con valores de tabla. Se muestran las siguientes columnas:  
  
-   **Nombre de parámetro** : muestra el nombre del parámetro definido por el procedimiento almacenado o la función con valores de tabla.  
  
-   **Valor** : valor que se usa para el parámetro cuando la consulta se ejecuta a fin de recuperar los datos que deben mostrarse en el panel Resultados de la consulta en tiempo de diseño. Este valor no se usa cuando el informe se ejecuta en el tiempo de ejecución.  
  
###  <a name="Relationships"></a> Panel Relaciones  
 El panel Relaciones muestra las relaciones de la combinación. Las relaciones pueden detectarse automáticamente en las relaciones de clave externa que se recuperan a partir de los metadatos de base de datos, o bien puede crearlas usted mismo.  
  
 Se muestran las siguientes opciones:  
  
-   **Detección automática** : alterna la característica de detección automática que crea automáticamente las relaciones entre las tablas. Si se activa la detección automática, el diseñador de consultas crea las relaciones a partir de las claves externas de las tablas; de lo contrario, debe crearlas manualmente. Al seleccionar las tablas en el panel **Vista de base de datos** , la detección automática intenta crear las relaciones automáticamente. Si activa la detección automática después de haber creado combinaciones manualmente, estas se descartarán.  
  
    > [!IMPORTANT]  
    >  Cuando se usa con [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)] , no se proporcionan los metadatos necesarios para crear las combinaciones y las relaciones no se pueden detectar automáticamente. Si una consulta recupera los datos de [!INCLUDE[ssDWCurrentFull](../../../includes/ssdwcurrentfull-md.md)], todas las combinaciones de la tabla deben crearse de forma manual.  
  
-   **Agregar relación** : agrega una relación a la lista **Relación** .  
  
     Si la detección automática está activada, las tablas cuyas columnas se utilizan en la consulta se agregan automáticamente a la lista **Relación** . Cuando la detección automática identifica que dos tablas están relacionadas, una se agrega a la columna **Tabla izquierda** , la otra a la columna **Tabla derecha** y entre ellas se crea una combinación interna. Cada relación genera una cláusula JOIN en la consulta. Si las tablas no están relacionadas, todas aparecen en la columna **Tabla izquierda** y la columna **Tipo de combinación** indica que las tablas no están relacionadas con otras. Cuando la detección automática está activada, no puede agregar manualmente relaciones entre las tablas que la detección automática determine que no están relacionadas.  
  
     Si se desactiva, puede agregar y cambiar las relaciones entre las tablas. Haga clic en **Campos de edición** para especificar los campos que se usarán para combinar las dos tablas.  
  
     El orden en el que las relaciones aparecen en la lista **Relación** es el orden en el que las combinaciones se realizarán en la consulta. Puede cambiar el orden de las relaciones moviéndolas arriba y abajo en la lista.  
  
     Cuando se usan varias relaciones en una consulta, en las relaciones anteriores debe hacerse referencia  a una de las tablas de cada relación, excepto la primera.  
  
     Si una relación anterior hace referencia a ambas tablas en una relación, la relación no genera una cláusula de combinación independiente; en su lugar se agrega una condición de combinación a la cláusula de combinación generada para la relación anterior. La relación anterior que hizo referencia a las mismas tablas se usa para inferir el tipo de combinación.  
  
-   **Campos de edición** : abre cuadro de diálogo **Editar campos relacionados** en el que puede agregar y modificar las relaciones entre las tablas. Los campos se eligen en las tablas derecha e izquierda que se combinan. Puede combinar varios campos de la tabla izquierda y de la tabla derecha para especificar varias condiciones de combinación en una relación. No es necesario que los dos campos que combinan la tabla izquierda y la tabla derecha tengan el mismo nombre. Los campos combinados deben tener tipos de datos compatibles.  
  
-   **Eliminar relación**  : elimina la relación seleccionada **.**  
  
-   **Subir** y **Bajar** : mueve las relaciones arriba o abajo en la lista **Relación** . La secuencia en la que las relaciones se colocan en la consulta puede afectar a sus resultados. Las relaciones se agregan a la consulta en el orden en que aparecen en la lista **Relación** .  
  
 Se muestran las siguientes columnas:  
  
-   **Tabla izquierda** : muestra el nombre de la primera tabla que forma parte de una relación de combinación.  
  
-   **Tipo de combinación** : muestra el tipo de instrucción JOIN de SQL que se usa en la consulta generada automáticamente. De forma predeterminada, si se detecta una restricción de clave externa, se utiliza INNER JOIN. Otros tipos de combinación pueden ser LEFT JOIN o RIGHT JOIN. Si no se aplica ninguno de estos tipos de combinación, la columna **Tipo de combinación** muestra **No relacionada**. No se crea ninguna combinación CROSS JOIN para las tablas no relacionadas; en su lugar, debe crear las relaciones manualmente combinando las columnas de las tablas izquierda y derecha. Para obtener más información acerca de los tipos de combinaciones JOIN, vea el tema sobre aspectos básicos de las combinaciones en los [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [Libros en pantalla](https://go.microsoft.com/fwlink/?LinkId=141687) en msdn.microsoft.com.  
  
-   **Tabla derecha** : muestra el nombre de la segunda tabla que forma parte de una relación de combinación.  
  
-   **Campos de combinación** : muestra los pares de campos combinados; si una relación tiene varias condiciones de combinación, los pares de campos combinados están separados por comas (,).  
  
###  <a name="AppliedFilters"></a> Panel Filtros aplicados  
 El panel Filtros aplicados muestra los criterios que se usan para limitar el número de filas de datos que deben recuperarse en tiempo de ejecución. Los criterios especificados en este panel se usan para generar una cláusula WHERE de SQL. Al seleccionar la opción de parámetro, se crea automáticamente un parámetro de informe. Los parámetros de informe basados en los parámetros de consulta permiten a un usuario especificar valores para que la consulta controle los datos del informe.  
  
 Se muestran las siguientes columnas:  
  
-   **Nombre de campo** : muestra el nombre del campo al que deben aplicarse los criterios.  
  
-   **Operador** : muestra la operación que debe usarse en la expresión de filtro.  
  
-   **Valor** : muestra el valor que debe usarse en la expresión de filtro.  
  
-   **Parámetro** : muestra la opción de agregar un parámetro de consulta a la consulta. Use las propiedades del conjunto de datos para ver la relación que existe entre el parámetro de consulta y el parámetro de informe.  
  
###  <a name="QueryResults"></a> Panel Resultados de la consulta  
 El panel Resultados de la consulta muestra los resultados de la consulta generada automáticamente que se especifica mediante selecciones en los otros paneles. Las columnas del conjunto de resultados son los campos que se especifican en el panel Campos seleccionados y los datos de fila quedan limitados por los filtros especificados en el panel Filtros aplicados. Si la consulta incluye agrega el conjunto de resultados incluye las nuevas columnas agregadas. Por ejemplo, si la columna **Color** se agrega utilizando el agregado Count, los resultados de la consulta incluyen una nueva columna. De forma predeterminada, esta columna se denomina **Count_Color**.  
  
 Estos datos representan los valores del origen de datos en el momento de ejecución de la consulta. Los datos no se guardan en la definición de informe. Los datos reales del informe se recuperar al procesar el informe.  
  
 El criterio de ordenación del conjunto de resultados se determina según el orden de los datos recuperados del origen de datos. El criterio de ordenación puede cambiarse modificando la consulta o después de recuperar los datos para el informe.  
  
### <a name="graphical-query-designer-toolbar"></a>Barra de herramientas del diseñador gráfico de consultas  
 La barra de herramientas del diseñador de consultas relacionales ofrece los siguientes botones para ayudarle a especificar o ver los resultados de una consulta.  
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|Cambie al diseñador de consultas basado en texto para ver la consulta generada automáticamente o para modificar la consulta.|  
|**Importar**|Importe una consulta existente de un archivo o informe. Solo se admiten los tipos de archivo .sql y .rdl.|  
|**Ejecutar consulta**|Ejecuta la consulta. El panel Resultados de la consulta muestra el conjunto de resultados.|  
  
## <a name="understanding-automatically-generated-queries"></a>Descripción de las consultas generadas automáticamente  
 Al seleccionar tablas y columnas, o procedimientos almacenados y vistas en el panel Vista de base de datos, el diseñador de consultas recupera la clave principal subyacente y las relaciones de clave externa del esquema de la base de datos. Al analizar estas relaciones, el diseñador de consultas detecta las relaciones entre dos tablas y agrega las combinaciones a la consulta. A continuación, puede modificar la consulta agregando grupos y agregados, agregando o cambiando relaciones, y agregando filtros. Para ver el texto de la consulta que muestra las columnas de las que recuperar los datos, las combinaciones entre las tablas y cualquier grupo o agregado, haga clic en **Editar como texto**.  
  
## <a name="text-based-query-designer"></a>Diseñador de consultas basado en texto  
 Para obtener el máximo control sobre la consulta, use el diseñador de consultas basado en texto. Para cambiar al diseñador de consultas basado en texto, en la barra de herramientas, haga clic en **Editar como texto**. Una vez que haya modificado una consulta en el diseñador de consultas basado en texto, ya no podrá usar el diseñador de consultas relacionales. La consulta se abrirá siempre en el diseñador de consultas basado en texto. Para más información, vea [Interfaz de usuario del Diseñador de consultas basado en texto &#40;Generador de informes&#41;](text-based-query-designer-user-interface-report-builder.md).  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores de consultas &#40;Generador de informes&#41;](../query-designers-report-builder.md)  
  
  
