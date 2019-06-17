---
title: Interfaz de usuario del diseñador gráfico de consultas | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10012"
- sql12.rtp.rptdesigner.dataview.vdtquerydesigner.f1
helpviewer_keywords:
- graphical query designer [Reporting Services]
- data sources [Reporting Services], creating
- text-based query designer [Reporting Services]
- query designers [Reporting Services]
- Reporting Services, query designers
ms.assetid: 5022ae33-03a3-48de-8ac1-82742f48cebe
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e6324606dea5f3ea6f094e9b3c3dbe31d5fbcf92
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107261"
---
# <a name="graphical-query-designer-user-interface"></a>Interfaz de usuario del diseñador gráfico de consultas
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona un diseñador gráfico de consultas y un diseñador de consultas basado en texto con los que se pueden crear consultas y recuperar datos de una base de datos relacional para un conjunto de datos de informe del Diseñador de informes. Use el diseñador gráfico de consultas para generar una consulta de forma interactiva y ver los resultados para los tipos de orígenes de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], Oracle, OLE DB y ODBC. Use el diseñador de consultas basado en texto para especificar varias instrucciones de [!INCLUDE[tsql](../../../includes/tsql-md.md)] , sintaxis compleja de consultas o comandos, y consultas basadas en expresiones. Para más información, vea [Interfaz de usuario del Diseñador de consultas basado en texto](../text-based-query-designer-user-interface.md). Para obtener más información sobre cómo trabajar con tipos de orígenes de datos específicos, consulte [agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-datasets-ssrs.md).  
  
 .  
  
## <a name="graphical-query-designer"></a>Diseñador gráfico de consultas  
 Este diseñador gráfico de consultas admite tres tipos de comandos de consulta: **Texto**, **StoredProcedure**, o **TableDirect**. Antes de crear una consulta para el conjunto de datos, debe seleccionar una opción de tipo de comando en la página Consulta del cuadro de diálogo [Propiedades del conjunto de datos](../dataset-properties-dialog-box-query.md) .  
  
 Dispone de tres tipos de consultas:  
  
-   El tipo**Text** admite texto de consultas estándar de [!INCLUDE[tsql](../../../includes/tsql-md.md)] para orígenes de datos de bases de datos relacionales, incluidas las extensiones de procesamiento de datos para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y Oracle.  
  
-   El tipo**TableDirect** selecciona todas las columnas de la tabla especificada. Por ejemplo, para una tabla denominada Customers, éste es el equivalente de la instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] de `SELECT * FROM Customers`.  
  
-   El tipo**StoredProcedure** admite llamadas a procedimientos almacenados en el origen de datos. Para usar esta opción, el administrador de la base de datos debe haberle concedido permiso de ejecución en el procedimiento almacenado para el origen de datos.  
  
 El tipo de comando predeterminado es **Text**.  
  
> [!NOTE]  
>  No todas las extensiones de procesamiento de datos admiten todos los tipos. El proveedor de datos subyacentes debe admitir un tipo de comando antes de que la opción esté disponible.  
  
### <a name="command-type-text"></a>Tipo de comando Text  
 En el tipo **Text** , el diseñador gráfico de consultas presenta cuatro áreas o paneles. En una consulta de [!INCLUDE[tsql](../../../includes/tsql-md.md)] , puede especificar columnas, alias, valores de ordenación y valores de filtro. Asimismo, puede ver el texto de consulta generado a partir de las selecciones, ejecutar la consulta y ver el conjunto de resultados. La figura siguiente muestra los cuatro paneles.  
  
 ![Diseñador gráfico de consultas para consultas SQL](../media/rsqd-dsaw-sql.gif "Diseñador gráfico de consultas para consultas SQL")  
  
 En la siguiente tabla se describe la función de cada panel.  
  
|Panel|Función|  
|----------|--------------|  
|Diagrama|Muestra las representaciones gráficas de las tablas de la consulta. Utilice este panel para seleccionar campos y definir relaciones entre tablas.|  
|Cuadrícula|Muestra una lista de los campos devueltos por la consulta. Use este panel para definir alias, criterios de ordenación, filtros, grupos y parámetros.|  
|SQL|Muestra la consulta de [!INCLUDE[tsql](../../../includes/tsql-md.md)] representada mediante los paneles de diagrama y de cuadrícula. Use este panel para escribir o actualizar una consulta mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)].|  
|Resultado|Muestra los resultados de la consulta. Para ejecutar la consulta, haga clic con el botón derecho en cualquier panel y, después, haga clic en **Ejecutar**, o bien haga clic en el botón **Ejecutar** en la barra de herramientas.|  
  
 Si cambia información en cualquiera de los tres primeros paneles, dichos cambios aparecerán en los demás paneles. Por ejemplo, si agrega una tabla en el panel Diagrama, ésta se agregará automáticamente a la consulta de [!INCLUDE[tsql](../../../includes/tsql-md.md)] del panel de SQL. Si se agrega un campo a la consulta del panel de SQL, se agrega automáticamente el campo a la lista del panel Cuadrícula y se actualiza la tabla del panel Diagrama.  
  
 Para más información, vea [Herramientas Diseñador de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md).  
  
#### <a name="toolbar-for-the-graphical-query-designer"></a>Barra de herramientas del diseñador gráfico de consultas  
 La barra de herramientas del diseñador gráfico de consultas proporciona botones que le ayudan a diseñar consultas de [!INCLUDE[tsql](../../../includes/tsql-md.md)] mediante la interfaz gráfica.  
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|Alterna entre el diseñador de consultas basado en texto y el diseñador gráfico de consultas.|  
|**Importar**|Importe una consulta existente de un archivo o informe. Solo se admiten los tipos de archivos .sql y .rdl. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Botón de alternancia Mostrar u ocultar panel de diagrama](../media/rsqdicon-showhidediagram.gif "Botón de alternancia Mostrar u ocultar panel de diagrama")|Muestra u oculta el panel Diagrama.|  
|![Botón de alternancia Mostrar u ocultar panel de cuadrícula](../media/rsqdicon-showhidegrid.gif "Botón de alternancia Mostrar u ocultar panel de cuadrícula")|Muestra u oculta el panel Cuadrícula.|  
|![Botón de alternancia Mostrar u ocultar panel de SQL](../media/rsqdicon-showhidesql.gif "Botón de alternancia Mostrar u ocultar panel de SQL")|Muestra u oculta el panel de SQL.|  
|![Botón de alternancia Mostrar u ocultar panel de resultados](../media/rsqdicon-showhideresult.gif "Botón de alternancia Mostrar u ocultar panel de resultados")|Muestra u oculta el panel Resultado.|  
|![Ejecutar la consulta](../../analysis-services/media/rsqdicon-run.gif "Ejecutar la consulta")|Ejecuta la consulta.|  
|![Botón Comprobar SQL en el panel de SQL](../media/rsqdicon-verifysql.gif "Botón Comprobar SQL en el panel de SQL")|Comprueba que la sintaxis del texto de consulta sea correcta.|  
|![Establecer orden ascendente en el campo seleccionado](../media/rsqdicon-sortascending.gif "Establecer orden ascendente en el campo seleccionado")|Establece el criterio de ordenación en **Orden ascendente** para la columna seleccionada en el panel Diagrama.|  
|![Establecer orden descendente en el campo seleccionado](../media/rsqdicon-sortdescending.gif "Establecer orden descendente en el campo seleccionado")|Establece el criterio de ordenación en **Orden descendente** para la columna seleccionada en el panel Diagrama.|  
|![Quitar filtro del campo seleccionado](../media/rsqdicon-removefilter.gif "Quitar filtro del campo seleccionado")|Quita el filtro para la columna seleccionada en el panel de diagrama que está marcado como filtrado (![Gráfico de filtro junto a la columna de filtro seleccionada](../media/rsqdicon-filter.gif "Gráfico de filtro junto a la columna de filtro seleccionada")).|  
|![Usar Agrupar por para el campo seleccionado](../media/rsqdicon-usegroupby.gif "Usar Agrupar por para el campo seleccionado")|Muestra u oculta la columna **Agrupar por** en el panel Cuadrícula. Cuando el botón de alternancia **Agrupar por** está activado, aparece una columna adicional llamada **Agrupar por** en el panel Cuadrícula; cada valor de las columnas seleccionadas de la consulta tiene el valor predeterminado **Agrupar por**, que hace que la columna seleccionada se incluya en una cláusula GROUP BY del texto SQL. Utilice el botón Agrupar por para agregar automáticamente una cláusula GROUP BY que incluya todas las columnas en la cláusula SELECT. Cuando la cláusula SELECT incluya llamadas de función de agregado (por ejemplo, SUM(nombreDeColumna)), incluya cada columna que no sea de agregado en la cláusula GROUP BY si desea que aparezca en el conjunto de resultados.<br /><br /> Para que aparezca en el panel Resultado, cada columna de la consulta debe tener una función de agregado definida para utilizarse en el cálculo del valor que se mostrará en dicho panel. De lo contrario, la columna de la consulta debe especificarse en la cláusula GROUP BY de la consulta SQL.|  
|![Agregar una nueva tabla al panel de diagrama](../media/rsqdicon-addtable.gif "Agregar una nueva tabla al panel de diagrama")|Agrega una nueva tabla del origen de datos al panel Diagrama.<br /><br /> **Nota** Cuando agrega una nueva tabla, el diseñador de consultas intenta hacer que coincidan las relaciones de clave externa del origen de datos. Después de agregar una tabla, confirme que las relaciones de clave externa, representadas por los vínculos entre las tablas, sean correctas.|  
  
#### <a name="example"></a>Ejemplo  
 La siguiente consulta devuelve la lista de apellidos de la tabla [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] Person **de la base de datos** :  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 También puede ejecutar procedimientos almacenados desde el panel de SQL. La siguiente consulta ejecuta el procedimiento almacenado **uspGetWhereUsedProductID** de la base de datos [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] :  
  
```  
EXEC uspGetEmployeeManagers '1';  
```  
  
### <a name="command-type-tabledirect"></a>Tipo de comando TableDirect  
 En el tipo **TableDirect** , el diseñador gráfico de consultas muestra una lista desplegable de las tablas disponibles del origen de datos y el panel Resultado. Si selecciona una tabla y hace clic en el botón **Ejecutar** , se devolverán todas las columnas de dicha tabla.  
  
> [!NOTE]  
>  la característica TableDirect solo es compatible con los tipos de orígenes de datos **OLE DB** y **ODBC** .  
  
 En la siguiente tabla se describe la función de cada panel.  
  
|Panel|Función|  
|----------|--------------|  
|Lista desplegable de tablas|Muestra todas las tablas disponibles del origen de datos. Seleccione uno de la lista para activarlo.|  
|Resultado|Muestra todas las columnas de la tabla seleccionada. Para ejecutar la consulta de tabla, haga clic en el botón **Ejecutar** de la barra de herramientas.|  
  
#### <a name="toolbar-buttons-for-the-command-type-tabledirect"></a>Botones de la barra de herramientas del tipo de comando TableDirect  
 La barra de herramientas del diseñador gráfico de consultas proporciona una lista desplegable de tablas en el origen de datos. La tabla siguiente contiene una lista con todos los botones y sus funciones.  
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|Alterna entre el diseñador de consultas basado en texto y el diseñador gráfico de consultas.|  
|**Importar**|Importe una consulta existente de un archivo o informe. Solo se admiten los tipos de archivos .sql y .rdl. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Icono del botón Diseñador de consultas genérico](../media/icongenericquerydesigner.gif "Icono del botón Diseñador de consultas genérico")|Alterna el diseñador de consultas genérico y el diseñador gráfico de consultas, a la vez que mantiene el texto de consulta o la vista del procedimiento almacenado.|  
|![Ejecutar la consulta](../../analysis-services/media/rsqdicon-run.gif "Ejecutar la consulta")|Selecciona todas las columnas de la tabla seleccionada.|  
  
### <a name="command-type-storedprocedure"></a>Tipo de comando StoredProcedure  
 En el tipo **StoredProcedure** , el diseñador gráfico de consultas muestra una lista desplegable de los procedimientos almacenados disponibles del origen de datos y el panel Resultado. En la siguiente tabla se describe la función de cada panel.  
  
|Panel|Función|  
|----------|--------------|  
|Lista desplegable de procedimientos almacenados|Muestra todos los procedimientos almacenados disponibles del origen de datos. Seleccione uno de la lista para activarlo.|  
|Resultado|Muestra el resultado de la ejecución del procedimiento almacenado. Para ejecutar el procedimiento almacenado seleccionado, haga clic en el botón **Ejecutar** de la barra de herramientas.|  
  
#### <a name="toolbar-buttons-for-command-type-storedprocedure"></a>Botones de la barra de herramientas del tipo de comando StoredProcedure  
 La barra de herramientas del diseñador gráfico de consultas proporciona una lista desplegable de procedimientos almacenados en el origen de datos. La tabla siguiente contiene una lista con todos los botones y sus funciones.  
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|Alterna entre el diseñador de consultas basado en texto y el diseñador gráfico de consultas.|  
|**Importar**|Importe una consulta existente de un archivo o informe. Solo se admiten los tipos de archivos .sql y .rdl. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Ejecutar la consulta](../../analysis-services/media/rsqdicon-run.gif "Ejecutar la consulta")|Ejecuta el procedimiento almacenado.|  
|Lista desplegable de procedimientos almacenados|Haga clic en la flecha abajo para mostrar una lista de procedimientos almacenados disponibles del origen de datos. Haga clic en un procedimiento almacenado de la lista para seleccionarlo.|  
  
#### <a name="example"></a>Ejemplo  
 El siguiente procedimiento almacenado llama a una lista de cargos de los administradores de la base de datos [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] . Este procedimiento almacenado acepta *BusinessEntityID* como parámetro. Puede especificar un entero pequeño.  
  
 `uspGetEmployeeManagers '1';`  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de diseño de herramientas de datos del servidor de informes SQL Diseñador de consultas &#40;SSRS&#41;](query-design-tools-ssrs.md)   
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-datasets-ssrs.md)   
 [Tipo de conexión de SQL Server &#40;SSRS&#41;](sql-server-connection-type-ssrs.md)   
 [Tipo de conexión OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md)   
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-datasets-ssrs.md)   
 [Tipo de conexión de Oracle &#40;SSRS&#41;](oracle-connection-type-ssrs.md)   
 [Archivo de configuración RSReportDesigner](../report-server/rsreportdesigner-configuration-file.md)   
 [Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
