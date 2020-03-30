---
title: Editor de consultas del motor de base de datos
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.tsqlquery.f1
dev_langs:
- TSQL
helpviewer_keywords:
- Query Editor [Database Engine]
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Query Editor [Database Engine], Toolbar
- editors [SQL Server Management Studio], Database Engine Query Editor
- Query Editor [Database Engine], Features
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/03/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 685397689b390175bd15f6241fc7036004e1e97a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "79198542"
---
# <a name="ssms-query-editor"></a>Editor de consultas SSMS

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

El editor de consultas del Motor de base de datos es uno de los cuatro editores implementados en SQL Server Management Studio (SSMS).

Use el Editor de consultas para crear y ejecutar scripts que contengan instrucciones Transact-SQL. El editor también permite ejecutar scripts que contengan comandos **sqlcmd** .

Para obtener una descripción de la funcionalidad implementada en el Editor de consultas y las tareas principales que se pueden realizar mediante el editor, consulte [Editores de consultas y texto](../scripting/query-and-text-editors-sql-server-management-studio.md).

![Nueva consulta](media/database-engine-query-editor-sql-server-management-studio/new-query.png)

## <a name="transact-sql-f1-help"></a>Transact-SQL (Ayuda F1)

El Editor de consultas admite la vinculación al tema de referencia de una instrucción específica de Transact-SQL al seleccionar F1. Para ello, resalte el nombre de una instrucción Transact-SQL y presione F1. El motor de búsqueda de ayuda busca entonces un tema que tenga un atributo de ayuda F1 que coincida con la cadena resaltada.

Si el motor de búsqueda de ayuda no encuentra un tema con una palabra clave de ayuda F1 que coincida exactamente con la cadena resaltada, se mostrará este tema. En ese caso, hay dos métodos para encontrar la ayuda que busca:

- Copiar y pegar la cadena del editor que resaltó en la pestaña de búsqueda de los Libros en pantalla de SQL Server y realizar una búsqueda.

- Resaltar solo la parte de la instrucción Transact-SQL que sea más probable que coincida con una palabra clave de Ayuda F1 aplicada a un tema y vuelva a presionar F1. El motor de búsqueda requiere una correspondencia exacta entre la cadena resaltada y una palabra clave de Ayuda F1 asignada a un tema. Si la cadena resaltada contiene elementos únicos de su entorno, como nombres de columna o parámetro, el motor de búsqueda no obtendrá una coincidencia. Entre los ejemplos de cadenas que se van a resaltar se incluyen los siguientes:

  - El nombre de una instrucción Transact-SQL, como SELECT, CREATE DATABASE o BEGIN TRANSACTION.

  - El nombre de una función integrada, como SERVERPROPERTY o @@VERSION.

  - El nombre de una tabla de procedimiento almacenado del sistema o de una vista, como sys.data_spaces o sp_tableoption.

## <a name="sql-editor-toolbar"></a>Barra de herramientas del Editor SQL

Cuando el Editor de consultas está abierto, la barra de herramientas del Editor SQL aparece con los botones siguientes.

También puede agregar la barra de herramientas del Editor SQL seleccionando el menú **Ver** y, a continuación, las opciones **Barras de herramientas**y **Editor SQL**. Si agrega la barra de herramientas del Editor SQL cuando no está abierta ninguna ventana del Editor de consultas, no habrá ningún botón disponible.

![Barra de herramientas del editor](media/database-engine-query-editor-sql-server-management-studio/editor-toolbar.png)

### <a name="connect-using-the-editor-toolbar"></a>Conexión mediante la barra de herramientas del editor

Se abre el cuadro de diálogo **[Conectar al servidor](connect-to-server-database-engine.md)** . Utilice este cuadro de diálogo para establecer una conexión a un servidor.

También puede conectarse a la base de datos mediante el [menú contextual](#connection-using-the-context-menu).

### <a name="change-connection-using-the-editor-toolbar"></a>Cambio de la conexión mediante la barra de herramientas del editor

Se abre el cuadro de diálogo **Conectar al servidor** . Use este cuadro de diálogo para establecer una [conexión a un servidor diferente](f1-help-for-server-connections-sql-server-management-studio.md).

También puede cambiar las conexiones mediante el [menú contextual](#connection-using-the-context-menu).

### <a name="available-databases-using-the-editor-toolbar"></a>Bases de datos disponibles mediante la barra de herramientas del editor

Cambia la conexión a una base de datos distinta del mismo servidor.

### <a name="execute-using-the-editor-toolbar"></a>Ejecución mediante la barra de herramientas del editor

Ejecuta el código seleccionado o, si no se ha seleccionado ningún código, ejecuta todo el código del Editor de consultas.

También puede **ejecutar** una consulta con F5 o en el [menú contextual](#execute-using-the-context-menu).

### <a name="cancel-executing-query-using-the-editor-toolbar"></a>Cancelación de la ejecución de consultas mediante la barra de herramientas del editor

Envía una solicitud de cancelación al servidor. Algunas consultas no pueden cancelarse inmediatamente, sino que deben esperar a una condición de cancelación adecuada. Cuando se cancelan las transacciones, podrían producirse retrasos mientras se revierten.

También puede cancelar una consulta en ejecución si selecciona Alt + Interrumpir.

### <a name="parse-using-the-editor-toolbar"></a>Análisis mediante la barra de herramientas del editor

Comprueba la sintaxis del código seleccionado. Si no se ha seleccionado ningún código, comprueba la sintaxis de todo el código en la ventana del Editor de consultas.

También puede comprobar el código en el Editor de consultas con Ctrl + F5.

### <a name="display-estimated-execution-plan-using-the-editor-toolbar"></a>Visualización del plan de ejecución estimado mediante la barra de herramientas del editor

Solicita un plan de ejecución de consulta desde el procesador de consultas sin ejecutar realmente la consulta y muestra el plan en la ventana **Plan de ejecución** . Este plan utiliza estadísticas de índice para calcular el número de filas que se prevé que van a devolverse en cada parte de la ejecución de la consulta. El plan de consultas real que se utiliza puede ser diferente del plan de ejecución calculado. Esto puede ocurrir si el número de filas que se devuelven es significativamente diferente del calculado y el procesador de consultas cambia el plan para obtener una mayor eficacia.

También puede mostrar un plan de ejecución estimado con Ctrl + L o en el [menú contextual](#display-estimated-execution-plan-using-the-context-menu).

### <a name="query-options-using-the-editor-toolbar"></a>Opciones de consulta mediante la barra de herramientas del editor

Abre el cuadro de diálogo **Opciones de consulta** . Use este cuadro de diálogo para configurar las opciones predeterminadas de la ejecución de consultas y los resultados de las mismas.

También puede seleccionar **Opciones de consulta** en el [menú contextual](#query-options-using-the-context-menu).

### <a name="intellisense-enabled-using-the-editor-toolbar"></a>IntelliSense habilitado mediante la barra de herramientas del editor

Especifica si la funcionalidad de IntelliSense está disponible en el Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Esta opción está establecida de forma predeterminada.

También puede seleccionar **IntelliSense habilitado** si presiona Ctrl + B y luego Ctrl I, o bien en el [menú contextual](#intellisense-enabled-using-the-context-menu).

### <a name="include-actual-execution-plan-using-the-editor-toolbar"></a>Inclusión del plan de ejecución real mediante la barra de herramientas del editor

Ejecuta la consulta, devuelve los resultados de la consulta y el plan de ejecución que se usó para la consulta. Se muestran como un plan de consultas gráfico en la ventana **Plan de ejecución** .

También puede seleccionar **Incluir plan de ejecución real** con Ctrl + M o en el [menú contextual](#include-actual-execution-plan-using-the-context-menu).

### <a name="include-live-query-statistics-using-the-editor-toolbar"></a>Inclusión de estadísticas de consultas activas mediante la barra de herramientas del editor

Proporciona información en tiempo real sobre el proceso de ejecución de consultas a medida que los controles fluyen de un operador de plan de consulta a otro.

También puede seleccionar **Include Live Query Statistics** (Incluir estadísticas de consultas activas) en el [menú contextual](#include-live-query-statistics-using-the-context-menu).

### <a name="include-client-statistics-using-the-editor-toolbar"></a>Inclusión de estadísticas de cliente mediante la barra de herramientas del editor

Incluye una ventana **Estadísticas de clientes** que contiene estadísticas sobre la consulta y los paquetes de red, así como el tiempo transcurrido de la consulta.

También puede seleccionar **Include Live Query Statistics** (Incluir estadísticas de consultas activas) mediante Mayús + Alt + S o en el [menú contextual](#include-client-statistics-using-the-context-menu).

### <a name="results-to-text-using-the-editor-toolbar"></a>Resultados a texto mediante la barra de herramientas del editor

Devuelve los resultados de la consulta como texto en la ventana **Resultados** .

También puede devolver los resultados a texto con Ctrl + T o en el [menú contextual](#results-using-the-context-menu).

### <a name="results-to-grid-using-the-editor-toolbar"></a>Resultados a cuadrícula mediante la barra de herramientas del editor

Devuelve los resultados de la consulta como una o varias cuadrículas en la ventana **Resultados** . Esta opción está normalmente habilitada de manera predeterminada.

También puede devolver los resultados a texto con Ctrl + D o en el [menú contextual](#results-using-the-context-menu).

### <a name="results-to-file-using-the-editor-toolbar"></a>Resultados a archivo mediante la barra de herramientas del editor

Cuando se ejecuta la consulta, se abre el cuadro de diálogo **Guardar resultados** . En **Guardar en**, seleccione la carpeta en la que desea guardar el archivo. En **Nombre de archivo**, escriba el nombre del archivo y, luego, seleccione **Guardar** para guardar los resultados de la consulta como un archivo de **Informe** con la extensión .rpt. Para acceder a las opciones avanzadas, haga clic en la flecha abajo en el botón **Guardar** y, luego, seleccione **Guardar con codificación**.

También puede devolver los resultados a texto con Ctrl + Mayús + F o en el [menú contextual](#results-using-the-context-menu).

### <a name="comment-out-the-selected-lines-using-the-editor-toolbar"></a>Conversión en comentario de las líneas seleccionadas mediante la barra de herramientas del editor

Convierte la línea actual en comentario agregando al principio de la línea un operador de comentario (--).

También puede convertir en comentario una línea con Ctrl + K y Ctrl + C.

### <a name="uncomment-the-selected-lines-using-the-editor-toolbar"></a>Eliminación de las marcas de comentario de las líneas seleccionadas mediante la barra de herramientas del editor

Convierte la línea actual en una instrucción de código activo quitando los operadores de comentario (--) del principio de la línea.

También puede quitar la marca de comentario de una línea si presiona Ctrl + K y, luego, Ctrl + U.

### <a name="decrease-indent-using-the-editor-toolbar"></a>Reducción de la sangría mediante la barra de herramientas del editor

Mueve el texto de la línea a la izquierda quitando los espacios en blanco al principio de la línea.

### <a name="increase-line-indent-using-the-editor-toolbar"></a>Aumento de la sangría de línea mediante la barra de herramientas del editor

Mueve el texto de la línea a la derecha agregando espacios en blanco al principio de la línea.

### <a name="specify-values-for-template-parameters-using-the-editor-toolbar"></a>Especificación de los valores de los parámetros de plantilla mediante la barra de herramientas del editor

Abre un cuadro de diálogo que puede utilizar para especificar los valores de los parámetros en los procedimientos almacenados y funciones.

## <a name="context-menu"></a>Menú contextual

Puede acceder al menú contextual si *hace clic con el botón derecho* en cualquier parte del Editor de consultas. Las opciones del menú contextual son similares a las de la barra de herramientas del Editor SQL. Con el menú contextual, verá las mismas opciones que **Conectar** y **Ejecutar**, pero también obtiene otras opciones, como **Insertar fragmento de código** y **Envolver con**.

![Opciones del menú contextual](media/database-engine-query-editor-sql-server-management-studio/context-menu.png)

### <a name="insert-snippet-using-the-context-menu"></a>Inserción de un fragmento de código mediante el menú contextual

Un fragmento de código de Transact-SQL es una plantilla que se puede usar como un punto inicial al escribir nuevas instrucciones de Transact-SQL en el Editor de consultas.

### <a name="surround-with-using-the-context-menu"></a>Envolver con mediante el menú contextual

Un fragmento de código "envolver con" es una plantilla que puede usar como punto de partida al encerrar un conjunto de instrucciones de Transact-SQL en un bloque BEGIN, IF o WHILE.

### <a name="connection-using-the-context-menu"></a>Conexión mediante el menú contextual

![Opciones del menú contextual](media/database-engine-query-editor-sql-server-management-studio/context-menu-connections.png)

Hay más opciones de **Conexión** en el menú contextual en comparación con las opciones de la barra de herramientas de SSMS.

- **Conectar**: abre el cuadro de diálogo Conectar al servidor. Utilice este cuadro de diálogo para establecer una conexión a un servidor.

- **Desconectar**: desconecta el Editor de consultas actual del servidor.

- **Desconectar todas las consultas**: desconecta todas las conexiones de consulta.

- **Cambiar conexión**: abre el cuadro de diálogo Conectar al servidor. Utilice este cuadro de diálogo para establecer una conexión a un servidor diferente.

### <a name="open-server-in-object-explorer-using-the-context-menu"></a>Apertura del servidor en el Explorador de objetos mediante el menú contextual

El Explorador de objetos proporciona un interfaz jerárquica para ver y administrar los objetos de cada instancia de SQL Server. El panel Detalles del Explorador de objetos muestra una vista tabular de los objetos de instancia y la capacidad de buscar objetos específicos. Las funciones del Explorador de objetos varían ligeramente según el tipo de servidor, aunque, por lo general, incluyen características de desarrollo de bases de datos y características de administración para todo tipo de servidores.

### <a name="execute-using-the-context-menu"></a>Ejecución mediante el menú contextual

Ejecuta el código seleccionado o, si no se ha seleccionado ningún código, ejecuta todo el código del Editor de consultas.

### <a name="display-estimated-execution-plan-using-the-context-menu"></a>Visualización del plan de ejecución estimado mediante el menú contextual

Solicita un plan de ejecución de consulta desde el procesador de consultas sin ejecutar realmente la consulta y muestra el plan en la ventana **Plan de ejecución** . Este plan utiliza estadísticas de índice para calcular el número de filas que se prevé que van a devolverse en cada parte de la ejecución de la consulta. El plan de consultas real que se utiliza puede ser diferente del plan de ejecución calculado. Esto puede ocurrir si el número de filas que se devuelven es significativamente diferente del calculado y el procesador de consultas cambia el plan para obtener una mayor eficacia.

### <a name="intellisense-enabled-using-the-context-menu"></a>IntelliSense habilitado mediante el menú contextual

Especifica si la funcionalidad de IntelliSense está disponible en el Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Esta opción está establecida de forma predeterminada.

### <a name="trace-query-in-sql-server-profiler-using-the-context-menu"></a>Seguimiento de consultas en SQL Server Profiler mediante el menú contextual

SQL Server Profiler es una interfaz para crear y administrar seguimientos y analizar y reproducir resultados de seguimiento. Los eventos se guardan en un archivo de seguimiento que posteriormente se puede analizar o utilizar para reproducir una serie de pasos específicos cuando se intenta diagnosticar un problema.

### <a name="analyze-query-in-database-engine-tuning-advisor-using-the-context-menu"></a>Análisis de consultas en el Asistente para la optimización de motor de base de datos mediante el menú contextual

El Asistente para la optimización de motor de base de datos (DTA) de Microsoft analiza las bases de datos y hace recomendaciones que puede usar para optimizar el rendimiento de las consultas. Puede usar el Asistente para la optimización de motor de base de datos a fin de seleccionar y crear un conjunto óptimo de índices, vistas indexadas o particiones de tabla sin necesidad de conocer detalladamente la estructura de la base de datos ni el funcionamiento interno de SQL Server. Con DTA, puede realizar las siguientes tareas.

### <a name="design-query-in-editor-using-the-context-menu"></a>Diseño de consultas en el editor mediante el menú contextual

El Diseñador de consultas y vistas se ejecuta cuando se abre la definición de una vista, cuando se muestran los resultados de una consulta o una vista, o cuando se crea o se abre una consulta.

### <a name="include-actual-execution-plan-using-the-context-menu"></a>Inclusión del plan de ejecución real mediante el menú contextual

Ejecuta la consulta, devuelve los resultados de la consulta y el plan de ejecución que se usó para la consulta. Se muestran como un plan de consultas gráfico en la ventana **Plan de ejecución** .

### <a name="include-live-query-statistics-using-the-context-menu"></a>Inclusión de estadísticas de consultas activas mediante el menú contextual

Proporciona información en tiempo real sobre el proceso de ejecución de consultas a medida que los controles fluyen de un operador de plan de consulta a otro.

### <a name="include-client-statistics-using-the-context-menu"></a>Inclusión de estadísticas de cliente mediante el menú contextual

Incluye una ventana **Estadísticas de clientes** que contiene estadísticas sobre la consulta y los paquetes de red, así como el tiempo transcurrido de la consulta.

### <a name="results-using-the-context-menu"></a>Resultados mediante el menú contextual

![Opciones de resultados](media/database-engine-query-editor-sql-server-management-studio/context-menu-results.png)

Puede seleccionar cualquiera de las opciones de *Resultado* que prefiera en el menú contextual.

- **Resultados a texto**: devuelve los resultados de la consulta como texto en la ventana **Resultados**.

- **Resultados a cuadrícula**: devuelve los resultados de la consulta como una o varias cuadrículas en la ventana **Resultados**.

- **Resultados a archivo**: cuando se ejecuta la consulta, se abre el cuadro de diálogo **Guardar resultados**. En **Guardar en**, seleccione la carpeta en la que desea guardar el archivo. En **Nombre de archivo**, escriba el nombre del archivo y, luego, seleccione **Guardar** para guardar los resultados de la consulta como un archivo de **Informe** con la extensión .rpt. Para acceder a las opciones avanzadas, haga clic en la flecha abajo en el botón **Guardar** y, luego, seleccione **Guardar con codificación**.

### <a name="properties-window-using-the-context-menu"></a>Ventana de propiedades mediante el menú contextual

La [ventana de propiedades](../menu-help/properties-window-f1-help-management-studio.md) describe el estado de un elemento en SQL Server Management Studio, como una conexión o un operador de plan de presentación, y proporciona información sobre objetos de la base de datos, como tablas, vistas y diseñadores.

La ventana Propiedades se puede utilizar para ver las propiedades de la conexión actual. Muchas propiedades son de solo lectura en la ventana de propiedades, aunque se pueden cambiar en otra parte de Management Studio. Por ejemplo, la propiedad Database de una consulta es de solo lectura en la ventana Propiedades, aunque se puede cambiar en la barra de herramientas.

### <a name="query-options-using-the-context-menu"></a>Opciones de consulta mediante el menú contextual

Abre el cuadro de diálogo **Opciones de consulta** . Use este cuadro de diálogo para configurar las opciones predeterminadas de la ejecución de consultas y los resultados de las mismas.

## <a name="see-also"></a>Consulte también

- [Personalizar los menús y los métodos abreviados de teclado](../customize-menus-and-shortcut-keys.md)

- [Alternativas de SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)
