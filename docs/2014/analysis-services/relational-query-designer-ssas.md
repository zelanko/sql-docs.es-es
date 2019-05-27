---
title: Diseñador de consultas relacionales (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.relquerydesginer.f1
ms.assetid: 9399b1d1-1ad2-44df-bd11-bef60fbf01ec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8063df9c748ca6838cd21b0a5daa249fdc49134c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070462"
---
# <a name="relational-query-designer-ssas"></a>Diseñador de consultas relacionales (SSAS)
  El diseñador de consultas relacionales le ayuda a crear una consulta que especifica los datos que hay que recuperar de las bases de datos relacionales de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] y del [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)]. Use el diseñador gráfico de consultas para explorar los metadatos, crear la consulta de forma interactiva y ver los resultados de la misma.  Use el diseñador de consultas basado en texto para ver la consulta creada por el diseñador gráfico de consultas o para modificar una consulta. También puede importar una consulta existente de un archivo o informe.  
  
 Si lo prefiere, puede escribir la consulta en lenguaje SQL utilizando el editor basado en texto. Para cambiar al diseñador de consultas basado en texto, en la barra de herramientas, haga clic en **Editar como texto**. Una vez que haya modificado una consulta en el diseñador de consultas basado en texto, ya no podrá usar el diseñador gráfico de consultas.  
  
> [!NOTE]  
>  Para especificar una consulta para los tipos de orígenes de datos Oracle, OLE DB, ODBC y Teradata, debe usar el diseñador de consultas basado en texto.  
  
> [!IMPORTANT]  
>  Los usuarios tienen acceso a los orígenes de datos cuando crean y ejecutan las consultas. Debe conceder permisos mínimos para los orígenes de datos, por ejemplo permisos de solo lectura.  
>   
>  Para conectarse al origen de datos cuando se ejecuta una consulta se utilizan las credenciales del usuario actual, no las credenciales especificadas en la página Información de suplantación.  
  
## <a name="graphical-query-designer"></a>Diseñador gráfico de consultas  
 En el diseñador gráfico de consultas, puede explorar las tablas y vistas de base de datos, y construir de forma interactiva la instrucción SQL SELECT que especifica las tablas y columnas de base de datos de las que se van a recuperar los datos para un conjunto de datos. Debe elegir los campos que se incluirán en el conjunto de datos y, si lo desea, especificar los filtros que limitan los datos en el conjunto de datos. Puede especificar que los filtros se usan como parámetros y proporcionar el valor del filtro en tiempo de ejecución. Si elige varias tablas, el diseñador de consultas describe la relación entre conjuntos de dos.  
  
 El diseñador gráfico de consultas se divide en tres áreas. El diseño del diseñador de consultas cambia en función de si la consulta utiliza tablas o vistas, o bien funciones con valores de tabla o procedimientos almacenados.  
  
> [!NOTE]  
>  [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] no admite procedimientos almacenados o funciones con valores de tabla.  
  
 La figura siguiente muestra el diseñador gráfico de consultas cuando se utiliza con tablas o vistas.  
  
 ![Diseñador gráfico de consultas](media/rsqd-relational-graphical.gif "Diseñador gráfico de consultas")  
  
 La figura siguiente muestra el diseñador gráfico de consultas cuando se utiliza con funciones con valores de tabla o procedimientos almacenados.  
  
 ![Procedimiento almacenado en un diseñador gráfico de consultas](media/rs-relational-graphical-sp.gif "Procedimiento almacenado en un diseñador gráfico de consultas")  
  
 En la siguiente tabla se describe la función de cada panel.  
  
|Panel|Función|  
|----------|--------------|  
|[Vista de base de datos](#DatabaseView)|Muestra una vista jerárquica de tablas, vistas, procedimientos almacenados y funciones con valores de tabla organizados por esquema de la base de datos.|  
|[Campos seleccionados](#SelectedFields)|Muestra la lista de nombres de campo de base de datos de los elementos seleccionados en el panel Vista de base de datos. Estos campos se convierten en la colección de campos para el conjunto de datos.|  
|[Parámetros de función](#FunctionParameters)|Muestra la lista de parámetros de entrada para procedimientos almacenados o funciones con valores de tabla en el panel Vista de base de datos.|  
|[Relaciones](#Relationships)|Muestra una lista de relaciones que se infieren de los campos seleccionados para tablas o vistas en el panel Vista de base de datos o las relaciones que creó manualmente.|  
|[Filtros aplicados.](#AppliedFilters)|Muestra una lista de campos y criterios de filtro para tablas o vistas en la Vista de base de datos.|  
|[Resultados de la consulta](#QueryResults)|Muestra datos de ejemplo para el conjunto de resultados de la consulta generada automáticamente.|  
  
###  <a name="DatabaseView"></a> Panel Vista de base de datos  
 El panel Vista de base de datos muestra los metadatos de los objetos de base de datos que el usuario tiene permiso para ver, que se determinan mediante la conexión a un origen de datos y las credenciales. La vista jerárquica muestra objetos de base de datos organizados por esquema de la base de datos. Expanda el nodo de cada esquema para ver las tablas, vistas, procedimientos almacenados y funciones con valores de tabla. Expanda una tabla o vista para ver las columnas.  
  
###  <a name="SelectedFields"></a> Panel Campos seleccionados  
 El panel Campos seleccionados muestra los campos en el conjunto de datos y los grupos y agregados para incluir en la consulta.  
  
 Se muestran las siguientes opciones:  
  
-   **Campos seleccionados**: muestra los campos de base de datos seleccionados para tablas o vistas, o los parámetros de entrada para procedimientos almacenados o funciones con valores de tabla. Los campos que se muestran en este panel se convierten en la colección de campos para el conjunto de datos.  
  
     Utilice el panel Datos de informe para mostrar la colección de campos para un conjunto de datos.  
  
-   **Grupo y agregado** : alterna el uso de la agrupación y los agregados en la consulta. Si desactiva la característica de agrupación y agregados después de agregar agrupaciones y agregados, estos se quitan. El texto **(ninguno)** indica que no se usa ninguna agrupación ni agregados. Si activa de nuevo la característica de agrupación y agregados, se restauran las agrupaciones y agregados anteriores.  
  
-   **Eliminar campo** : elimina el campo seleccionado.  
  
#### <a name="group-and-aggregate"></a>Grupo y agregado  
 Las consultas a las bases de datos con una tabla grande podrían devolver un número de filas de datos que sea demasiado elevado para ser útil y afecte al rendimiento en la red que transporta la ingente cantidad de datos. Para limitar el número de filas de datos, la consulta puede incluir agregados de SQL que resumen los datos en el servidor de bases de datos.  
  
 Los agregados proporcionan resúmenes de datos y los datos se agrupan para admitir el agregado que ofrece los datos de resumen. Al utilizar un agregado en la consulta, los otros campos que devuelve se agrupan automáticamente y la consulta incluye la cláusula de SQL GROUP BY. Puede resumir los datos sin agregar un agregado utilizando solo la opción **Agrupar por** en la lista **Grupo y agregado** . Muchos de los agregados incluyen una versión que utiliza la palabra clave DISTINCT. Al incluir DISTINCT, se eliminan los valores duplicados.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa [!INCLUDE[tsql](../includes/tsql-md.md)] y de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] usa [!INCLUDE[DWsql](../includes/dwsql-md.md)]. Ambos dialectos del lenguaje SQL admiten la cláusula, la palabra clave y los agregados que el diseñador de consultas proporciona.  
  
 Para más información sobre [!INCLUDE[tsql](../includes/tsql-md.md)], vea [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference) en los [Libros en pantalla](https://go.microsoft.com/fwlink/?LinkId=141687) de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en msdn.microsoft.com.  
  
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
  
-   **Nombre de parámetro**: muestra el nombre del parámetro definido por el procedimiento almacenado o la función con valores de tabla.  
  
-   **Valor** : valor que se usa para el parámetro cuando la consulta se ejecuta a fin de recuperar los datos que deben mostrarse en el panel Resultados de la consulta en tiempo de diseño. Este valor no se usa en tiempo de ejecución.  
  
###  <a name="Relationships"></a> Panel Relaciones  
 El panel Relaciones muestra las relaciones de la combinación. Las relaciones pueden detectarse automáticamente en las relaciones de clave externa que se recuperan a partir de los metadatos de base de datos, o bien puede crearlas usted mismo.  
  
 Se muestran las siguientes opciones:  
  
-   **Detección automática** : alterna la característica de detección automática que crea automáticamente las relaciones entre las tablas. Si se activa la detección automática, el diseñador de consultas crea las relaciones a partir de las claves externas de las tablas; de lo contrario, debe crearlas manualmente. Al seleccionar las tablas en el panel **Vista de base de datos** , la detección automática intenta crear las relaciones automáticamente. Si activa la detección automática después de haber creado combinaciones manualmente, estas se descartarán.  
  
    > [!IMPORTANT]  
    >  Cuando se usa con [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] , no se proporcionan los metadatos necesarios para crear las combinaciones y las relaciones no se pueden detectar automáticamente. Si una consulta recupera los datos de [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)], todas las combinaciones de la tabla deben crearse de forma manual.  
  
-   **Agregar relación** : agrega una relación a la lista **Relación** .  
  
     Si la detección automática está activada, las tablas cuyas columnas se utilizan en la consulta se agregan automáticamente a la lista **Relación** . Cuando la detección automática identifica que dos tablas están relacionadas, una se agrega a la columna **Tabla izquierda** , la otra a la columna **Tabla derecha** y entre ellas se crea una combinación interna. Cada relación genera una cláusula JOIN en la consulta. Si las tablas no están relacionadas, todas aparecen en la columna **Tabla izquierda** y la columna **Tipo de combinación** indica que las tablas no están relacionadas con otras. Cuando la detección automática está activada, no puede agregar manualmente relaciones entre las tablas que la detección automática determine que no están relacionadas.  
  
     Si se desactiva, puede agregar y cambiar las relaciones entre las tablas. Haga clic en **Campos de edición** para especificar los campos que se usarán para combinar las dos tablas.  
  
     El orden en el que las relaciones aparecen en la lista **Relación** es el orden en el que las combinaciones se realizarán en la consulta. Puede cambiar el orden de las relaciones moviéndolas arriba y abajo en la lista.  
  
     Cuando se usan varias relaciones en una consulta, en las relaciones anteriores debe hacerse referencia  a una de las tablas de cada relación, excepto la primera.  
  
     Si una relación anterior hace referencia a ambas tablas en una relación, la relación no genera una cláusula de combinación independiente; en su lugar se agrega una condición de combinación a la cláusula de combinación generada para la relación anterior. La relación anterior que hizo referencia a las mismas tablas se usa para inferir el tipo de combinación.  
  
-   **Campos de edición** : abre cuadro de diálogo **Editar campos relacionados** en el que puede agregar y modificar las relaciones entre las tablas. Los campos se eligen en las tablas derecha e izquierda que se combinan. Puede combinar varios campos de la tabla izquierda y de la tabla derecha para especificar varias condiciones de combinación en una relación. No es necesario que los dos campos que combinan la tabla izquierda y la tabla derecha tengan el mismo nombre. Los tipos de datos de los campos combinados deben ser compatibles.  
  
-   **Eliminar relación**  : elimina la relación seleccionada **.**  
  
-   **Subir** y **Bajar** : mueve las relaciones arriba o abajo en la lista **Relación** . La secuencia en la que las relaciones se colocan en la consulta puede afectar a sus resultados. Las relaciones se agregan a la consulta en el orden en que aparecen en la lista **Relación** .  
  
 Se muestran las siguientes columnas:  
  
-   **Tabla izquierda** : muestra el nombre de la primera tabla que forma parte de una relación de combinación.  
  
-   **Tipo de combinación** : muestra el tipo de instrucción JOIN de SQL que se usa en la consulta generada automáticamente. De forma predeterminada, si se detecta una restricción de clave externa, se utiliza INNER JOIN. Otros tipos de combinación pueden ser LEFT JOIN o RIGHT JOIN. Si no se aplica ninguno de estos tipos de combinación, la columna **Tipo de combinación** muestra **No relacionada**. No se crea ninguna combinación CROSS JOIN para las tablas no relacionadas; en su lugar, debe crear las relaciones manualmente combinando las columnas de las tablas izquierda y derecha. Para obtener más información acerca de los tipos de combinaciones JOIN, vea el tema sobre aspectos básicos de las combinaciones en los [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Libros en pantalla](https://go.microsoft.com/fwlink/?LinkId=141687) en msdn.microsoft.com.  
  
-   **Tabla derecha** : muestra el nombre de la segunda tabla que forma parte de una relación de combinación.  
  
-   **Campos de combinación** : muestra los pares de campos combinados; si una relación tiene varias condiciones de combinación, los pares de campos combinados están separados por comas (,).  
  
###  <a name="AppliedFilters"></a> Panel Filtros aplicados  
 El panel Filtros aplicados muestra los criterios que se usan para limitar el número de filas de datos que deben recuperarse en tiempo de ejecución. Los criterios especificados en este panel se usan para generar una cláusula WHERE de SQL. Al seleccionar la opción de parámetro, se crea automáticamente un parámetro.  
  
 Se muestran las siguientes columnas:  
  
-   **Nombre de campo** : muestra el nombre del campo al que deben aplicarse los criterios.  
  
-   **Operador** : muestra la operación que debe usarse en la expresión de filtro.  
  
-   **Valor** : muestra el valor que debe usarse en la expresión de filtro.  
  
-   **Parámetro** : muestra la opción de agregar un parámetro de consulta a la consulta.  
  
###  <a name="QueryResults"></a> Panel Resultados de la consulta  
 El panel Resultados de la consulta muestra los resultados de la consulta generada automáticamente que se especifica mediante selecciones en los otros paneles. Las columnas del conjunto de resultados son los campos que se especifican en el panel Campos seleccionados y los datos de fila quedan limitados por los filtros especificados en el panel Filtros aplicados.  
  
 Estos datos representan los valores del origen de datos en el momento de ejecución de la consulta.  
  
 El criterio de ordenación del conjunto de resultados se determina según el orden de los datos recuperados del origen de datos. El criterio de ordenación se puede cambiar modificando el texto de la consulta directamente. Para obtener más información sobre cómo usar la cláusula GROUP BY en una consulta, vea "GROUP BY (Transact-SQL)" en los [Libros en pantalla de SQL Server](https://go.microsoft.com/fwlink/?linkid=98335).  
  
### <a name="graphical-query-designer-toolbar"></a>Barra de herramientas del diseñador gráfico de consultas  
 La barra de herramientas del diseñador gráfico de consultas ofrece los siguientes botones para ayudarle a especificar o ver los resultados de una consulta.  
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|Cambie al diseñador de consultas basado en texto para ver la consulta generada automáticamente o para modificar la consulta.|  
|**Importar**|Importe una consulta existente de un archivo o informe. Solo se admiten los tipos de archivo .sql y .rdl.|  
|**Ejecutar consulta**|Ejecuta la consulta. El panel Resultados de la consulta muestra el conjunto de resultados.|  
  
## <a name="understanding-automatically-generated-queries"></a>Descripción de las consultas generadas automáticamente  
 Al seleccionar tablas y columnas, o procedimientos almacenados y vistas en el panel Vista de base de datos, el diseñador de consultas recupera la clave principal subyacente y las relaciones de clave externa del esquema de la base de datos. Al analizar estas relaciones, el diseñador de consultas detecta las relaciones entre dos tablas y agrega las combinaciones a la consulta. A continuación, puede modificar la consulta agregando grupos y agregados, agregando o cambiando relaciones, y agregando filtros. Para ver el texto de la consulta que muestra las columnas de las que recuperar los datos, las combinaciones entre las tablas y cualquier grupo o agregado, haga clic en **Editar como texto**.  
  
## <a name="text-based-query-designer"></a>Diseñador de consultas basado en texto  
 El diseñador de consultas basado en texto proporciona un medio para especificar una consulta mediante el lenguaje de consulta admitido por el origen de datos, para ejecutar la consulta y para ver los resultados en tiempo de diseño. Puede especificar varias sintaxis de consulta, comandos o instrucciones SQL para extensiones de procesamiento de datos personalizadas, y consultas que se especifican como expresiones.  
  
 Dado que el diseñador de consultas basado en texto no procesa de antemano la consulta, puede adaptarse a cualquier tipo de sintaxis de la consulta. Es la herramienta de diseño de consultas predeterminada para muchos tipos de orígenes de datos.  
  
 El diseñador de consultas basado en texto muestra una barra de herramientas y los dos paneles siguientes:  
  
-   **Consulta** Muestra el texto de la consulta, el nombre de tabla o el nombre del procedimiento almacenado, dependiendo del tipo de consulta. No todos los tipos de consulta están disponibles para todos los tipos de origen de datos. Por ejemplo, el nombre de tabla solamente es compatible con el tipo de orígenes de datos OLE DB.  
  
-   **Resultado** Muestra los resultados de la ejecución de la consulta en tiempo de diseño.  
  
### <a name="text-based-query-designer-toolbar"></a>Barra de herramientas del diseñador de consultas basado en texto  
 El diseñador de consultas basado en texto proporciona una sola barra de herramientas para todos los tipos de comando. La tabla siguiente contiene una lista con los botones de la barra de herramientas y sus funciones.  
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|Alterna entre el diseñador de consultas basado en texto y el diseñador gráfico de consultas. No todos los tipos de orígenes de datos admiten diseñadores gráficos de consultas.|  
|**Importar**|Importe una consulta existente de un archivo o informe. Solo se admiten los tipos de archivos sql y rdl.|  
|![Ejecutar la consulta](media/rsqdicon-run.gif "Ejecutar la consulta")|Ejecuta la consulta y muestra el conjunto de resultados en el panel Resultado.|  
|**Tipo de comando**|Seleccione **Text**, **StoredProcedure**o **TableDirect**. Si un procedimiento almacenado tiene parámetros, el cuadro de diálogo **Definir parámetros de consulta** aparece al hacer clic en **Ejecutar** en la barra de herramientas; puede rellenar los valores según sea necesario.<br /><br /> Tenga en cuenta que si un procedimiento almacenado devuelve más de un conjunto de resultados, el primer conjunto de resultados se usa para rellenar el conjunto de datos. Tenga en cuenta también que <br />                      **TableDirect** solo está disponible para el tipo de origen de datos OLE DB.|  
  
#### <a name="command-type-text"></a>Tipo de comando Text  
 Al crear un conjunto de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , el diseñador de consultas relacionales se abre de forma predeterminada. Para cambiar al diseñador de consultas basado en texto, haga clic en el botón de alternancia **Editar como texto** de la barra de herramientas. El diseñador de consultas basado en texto consta de dos paneles: el panel Consulta y el panel Resultado. En la siguiente ilustración se indica el nombre de cada panel.  
  
 ![Diseñador de consultas genérico, para consultas de datos relacionales](media/rsqd-dsaw-sql-generic.gif "Diseñador de consultas genérico, para consultas de datos relacionales")  
  
 En la siguiente tabla se describe la función de cada panel.  
  
|Panel|Función|  
|----------|--------------|  
|Consultar|Muestra el texto de consulta SQL. Use este panel para escribir o editar una consulta SQL.|  
|Resultado|Muestra los resultados de la consulta. Para ejecutar la consulta, haga clic con el botón derecho en cualquier panel y haga clic en **Ejecutar**, o bien haga clic en el botón **Ejecutar** de la barra de herramientas.|  
  
#### <a name="example"></a>Ejemplo  
 La siguiente consulta devuelve la lista de nombres de una tabla denominada `ContactType`.  
  
```  
SELECT Name FROM ContactType  
```  
  
 Si hace clic en **Ejecutar** en la barra de herramientas, el comando del panel **Consulta** se ejecuta y los resultados, una lista de nombres, se muestran en el panel **Resultado** .  
  
#### <a name="command-type-storedprocedure"></a>Tipo de comando StoredProcedure  
 Si selecciona **Tipo de comando StoredProcedure**, el diseñador de consultas basado en texto presenta dos paneles: el panel Consulta y el panel Resultado. Escriba el nombre del procedimiento almacenado en el panel Consulta y haga clic en **Ejecutar** en la barra de herramientas. Si el procedimiento almacenado utiliza parámetros, se abre el cuadro de diálogo **Definir parámetros de consulta** . Escriba los valores de los parámetros para el procedimiento almacenado.  
  
 La figura siguiente muestra los paneles Consulta y Resultado al ejecutar un procedimiento almacenado. En este caso, los parámetros de entrada son constantes.  
  
 ![Procedimiento almacenado en un diseñador de consultas basado en texto](media/rs-relational-text-sp.gif "Procedimiento almacenado en un diseñador de consultas basado en texto")  
  
 En la siguiente tabla se describe la función de cada panel.  
  
|Panel|Función|  
|----------|--------------|  
|Consultar|Muestra el nombre del procedimiento almacenado y de los parámetros de entrada.|  
|Resultado|Muestra los resultados de la consulta. Para ejecutar la consulta, haga clic con el botón derecho en cualquier panel y haga clic en **Ejecutar**, o bien haga clic en el botón **Ejecutar** de la barra de herramientas.|  
  
#### <a name="example"></a>Ejemplo  
 La consulta siguiente llama a un procedimiento almacenado denominado `uspGetWhereUsedProductID`. Cuando el procedimiento almacenado tenga parámetros de entrada, al ejecutar la consulta debe proporcionar los valores de los parámetros.  
  
```  
uspGetWhereUsedProductID  
```  
  
 Haga clic en el botón **Ejecutar** (**!**). En la tabla siguiente proporciona un ejemplo de `uspGetWhereUsedProductID` parámetros para el que se proporcionan valores en el **definir parámetros de consulta** cuadro de diálogo.  
  
|||  
|-|-|  
|*@StartProductID*|820|  
|*@CheckDate*|20010115|  
  
#### <a name="command-type-tabledirect"></a>Tipo de comando TableDirect  
 Si selecciona **Tipo de comando TableDirect**, el diseñador de consultas basado en texto presenta dos paneles: el panel Consulta y el panel Resultado. Si selecciona una tabla y hace clic en el botón **Ejecutar** , se devolverán todas las columnas de dicha tabla.  
  
#### <a name="example"></a>Ejemplo  
 En el caso de un tipo de origen de datos OLE DB, la siguiente consulta del conjunto de datos devuelve un conjunto de resultados para todos los tipos de contacto de la tabla `ContactType`.  
  
 `ContactType`  
  
 Escribir el nombre de tabla `ContactType` es equivalente a crear la instrucción SQL `SELECT * FROM ContactType`.  
  
  
