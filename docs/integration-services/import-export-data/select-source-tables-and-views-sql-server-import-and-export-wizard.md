---
title: "Seleccionar tablas y vistas de origen (Asistente para importación y exportación de SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 600e734c11a597cdcbae0279e1604bd96ccfb06f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Seleccionar tablas y vistas de origen (Asistente para importación y exportación de SQL Server)
  Después de especificar que quiere copiar una tabla completa o después de proporcionar una consulta, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Seleccionar tablas y vistas de origen**. En esta página, seleccione las tablas y vistas que quiera copiar. A continuación, asigne las tablas de origen a las tablas de destino nuevas o existentes. Opcionalmente, revise la asignación de columnas individuales y obtenga una vista previa de los datos de ejemplo.

> [!TIP]
> Si tiene que copiar más de una base de datos u objetos de base de datos de SQL Server que no sean tablas y vistas, use el Asistente para copiar bases de datos en lugar del Asistente para importación y exportación. Para más información, vea [Usar el Asistente para copiar bases de datos](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>Captura de pantalla: si va a copiar tablas  
 En la siguiente captura de pantalla se muestra un ejemplo de la página **Seleccionar tablas y vistas de origen** del asistente después de seleccionar la opción **Copiar los datos de una o varias tablas o vistas** en la página **Especificar copia de tabla o consulta**. En la lista, se ven todas las tablas y vistas disponibles del origen de datos.
 
En este ejemplo, la lista **Origen** contiene todas las tablas de la base de datos de ejemplo AdventureWorks. La fila seleccionada muestra que el usuario quiere copiar la tabla **Sales.Customer** del origen en la nueva tabla **Sales.CustomerNew** del destino. 
   
 ![Página Seleccionar tablas del Asistente para importación y exportación](../../integration-services/import-export-data/media/select-tables1.png "Página Seleccionar tablas del Asistente para importación y exportación")
  
## <a name="screen-shot---if-you-provided-a-query"></a>Captura de pantalla: si proporcionó una consulta  
 La siguiente captura de pantalla muestra un ejemplo de la página **Seleccionar tablas y vistas de origen** del asistente después de seleccionar la opción **Escribir una consulta para especificar los datos que se van a transferir** en la página **Especificar copia de tabla o consulta**. La lista **Origen** contiene solo una fila, en la cual el elemento denominado `[Query]` representa la consulta que proporcionó en la página **Proporcionar una consulta de origen**.
 
En este ejemplo, el usuario quiere copiar los resultados de la consulta del origen en la tabla **Sales.CustomerNew** del destino.  
    
 ![Página Seleccionar tablas del Asistente para importación y exportación](../../integration-services/import-export-data/media/select-tables2.png "Página Seleccionar tablas del Asistente para importación y exportación")  

## <a name="select-source-and-destination-tables"></a>Seleccionar tablas de destino y origen 
**Source**  
Utilice las casillas para seleccionar en la lista las tablas y vistas disponibles que deben copiarse en el destino. De forma predeterminada, los datos del origen de datos se copian sin cambios. Si crea una tabla de destino nueva, el esquema para la nueva tabla (es decir, la lista de columnas y sus propiedades) también se copia sin cambios desde el origen de datos.

Si proporcionó una consulta, la lista contiene un solo elemento con el nombre `[Query]`. 

**Destino**  
 Seleccione una tabla de destino de la lista para cada tabla o consulta de origen, o escriba el nombre de una nueva tabla que quiera que cree el asistente. Si selecciona una tabla de destino existente, esta debe tener columnas con tipos de datos que sean compatibles con los datos de origen.  

> [!NOTE]
> Si detiene el asistente en este punto para crear una tabla de forma manual en la base de datos de destino con una herramienta externa (como  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]), la nueva tabla no será visible de forma inmediata en la lista de tablas de destino disponibles. Para actualizar la lista de tablas de destino, retroceda hasta la página **Seleccionar un destino** , vuelva a seleccionar la base de datos de destino para actualizar la lista de tablas y vistas disponibles y luego regrese a la página **Seleccionar tablas y vistas de origen** .  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Revisión de las asignaciones de columnas y obtención de una vista previa de los datos (opcional)
**Editar asignaciones**   
Si quiere, puede hacer clic en **Editar asignaciones** para ver el cuadro de diálogo **Asignaciones de columnas** de la tabla seleccionada. Use el cuadro de diálogo **Asignaciones de columnas** para hacer lo siguiente:
-   Revise la asignación de columnas individuales entre el origen y el destino.
-   Copie solo un subconjunto de columnas si selecciona **Omitir** para las columnas que no desea copiar.

Para más información, vea [Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Vista previa**  
Si quiere, puede hacer clic en **Vista previa** para obtener una vista previa de hasta 200 filas de datos de ejemplo en el cuadro de diálogo **Vista previa de los datos**. Esto confirma que el asistente va a copiar los datos que quiere copiar. Para más información, vea [Vista previa de los datos](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Después de obtener una vista previa de los datos, es posible que quiera cambiar las opciones que seleccionó en páginas anteriores del asistente. Para realizar estas modificaciones, vuelva a la página **Seleccionar tablas y vistas de origen** y después haga clic en **Atrás** para volver a las páginas anteriores en las que puede cambiar sus selecciones.  

## <a name="select-source-and-destination-tables-for-excel"></a>Seleccionar tablas de destino y origen para Excel

### <a name="excel-source-tables"></a>Tablas de origen de Excel
En la lista de vistas y tablas de origen para un origen de datos de Excel se incluyen dos tipos de objetos de Excel.
-   **Hojas de cálculo.** Los nombres de las hojas de cálculo van seguidos del signo de dólar ($) (por ejemplo, **"Hoja1$"**).
-   **Rangos con nombre.** Los rangos con nombre, si los hay, se enumeran por nombre.

Si quiere cargar datos desde un intervalo de celdas específico y sin nombre (por ejemplo, **[Hoja1$A1:B4]**) o con destino a ese intervalo, tendrá que escribir una consulta. Vuelva a la página **Especificar copia de tabla o consulta** y seleccione **Escribir una consulta para especificar los datos que se van a transferir**.

#### <a name="prepare-the-excel-source-data"></a>Preparar los datos de origen de Excel
Tanto si especifica una hoja de cálculo o un rango como la tabla de origen, el controlador lee los bloques *contiguos* de celdas, comenzando con la primera celda no vacía en la esquina superior izquierda de la hoja de cálculo o rango. Como resultado, no puede haber filas vacías en los datos de origen. Por ejemplo, no puede haber una fila vacía entre los encabezados de columna y las filas de datos. Si hay un título seguido de filas vacías en la parte superior de la hoja de cálculo por encima de los datos, no se puede consultar la hoja de cálculo. En Excel, tiene que asignar un nombre al rango de datos y consultar el rango con nombre en lugar de la hoja de cálculo.

### <a name="excel-destination-tables"></a>Tablas de destino de Excel
Si va a exportar datos a Excel, puede especificar el destino de una de las tres formas siguientes.
-   **Hoja de cálculo.** Para especificar una hoja de cálculo, anexe el carácter $ al final del nombre de la hoja y agregue delimitadores alrededor de la cadena (por ejemplo, **[Hoja1$]**).
-   **Rango con nombre.** Para especificar un rango con nombre, use simplemente el nombre del rango (por ejemplo, **MiRangoDeDatos**).
-   **Rango sin nombre.** Para especificar un rango de celdas al que no ha asignado un nombre, anexe el carácter $ al final del nombre de la hoja, agregue la especificación del rango y agregue delimitadores alrededor de la cadena (por ejemplo, **[Hoja1$A1:B4]**).

## <a name="special-considerations-for-excel-sources-and-destinations"></a>Consideraciones especiales para los orígenes y destinos de Excel
Si usa Excel como origen o destino, es una buena idea hacer clic en **Editar asignaciones** y revisar las asignaciones de tipos de datos de la página **Asignaciones de columnas** . 

**Tipos de datos en los libros de Excel**. Excel no es una base de datos típica. Sus columnas no tienen tipos de datos fijos. El asistente solo reconoce un conjunto limitado de tipos de datos en Excel: numérico, moneda, booleano, fecha y hora, cadena (255 caracteres o menos) y memorando (más de 255 caracteres). El asistente toma una muestra de un cierto número de filas (de manera predeterminada, las primeras ocho filas) en un origen de datos de Excel existente para intentar determinar el tipo de datos de cada columna.

Cuando el asistente tiene que realizar conversiones de tipo de datos explícitas para cargar desde Excel o en Excel, normalmente se muestra la página **Revisar asignación de tipos de datos** donde puede revisar esas conversiones. Entre estas conversiones, se pueden incluir las siguientes.
-   Conversión entre columnas numéricas de Excel de doble precisión y columnas numéricas de otros tipos.
-   Conversión entre columnas de cadena de Excel de 255 caracteres y columnas de cadena de diferentes longitudes.
-   Conversión entre columnas de cadena de Excel Unicode y columnas de cadena no Unicode que usan páginas de códigos específicas.

### <a name="special-considerations-for-excel-sources"></a>Consideraciones especiales para orígenes de Excel
**Valores nulos o que faltan en datos importados**. Cuando parece que una columna de Excel contiene tipos de datos mixtos en las primeras ocho filas que muestrea el asistente (por ejemplo, valores numéricos mezclados con valores de texto), el asistente elige el tipo de datos mayoritario como el tipo de datos de la columna y devuelve valores nulos para las celdas que contienen datos de otros tipos. No hay ninguna forma de cambiar este comportamiento del asistente.

**Cadenas truncadas en datos importados**. Cuando el asistente determina que una columna de Excel contiene datos de texto, el asistente selecciona el tipo de datos de la columna (cadena o memorando) en función del valor más largo que muestrea en las primeras ocho filas. Si el asistente no encuentra valores de más de 255 caracteres en las filas que muestrea, trata a la columna como una columna de cadenas de 255 caracteres en lugar de una columna de memorando y trunca los valores de más de 255 caracteres. Para importar datos desde una columna de memorando sin truncamiento, tendrá que asegurarse de que la columna de memorando contiene al menos un valor de más de 255 caracteres en las ocho primeras filas que muestrea el asistente.

### <a name="special-considerations-for-excel-destinations"></a>Consideraciones especiales para destinos de Excel
**Especificar un rango existente**. Al especificar un rango existente como destino, obtendrá un error si el rango tiene menos *columnas* que el origen de datos. En cambio, si el rango que especifica tiene menos *filas* que los datos de origen, el asistente sigue escribiendo filas y extiende la definición del rango para que coincida con el nuevo número de filas.

**Guardar datos de memorando (ntext)**. Para poder guardar correctamente cadenas de más de 255 caracteres en una columna de Excel, el asistente debe reconocer el tipo de datos de la columna de destino como **memorando** y no como **cadena**.
-   Si la tabla de destino ya contiene filas de datos, las ocho primeras filas que muestree el asistente deberán contener por lo menos una fila con un valor de más de 255 caracteres en la columna de memorando.
-   Si el asistente crea la tabla de destino, la instrucción **CREATE TABLE** deberá usar **LONGTEXT** (o uno de sus sinónimos) como tipo de datos de la columna de memorando. Compruebe la instrucción **CREATE TABLE** y revísela si es necesario. Para ello, haga clic en **Editar SQL** junto a la opción **Crear tabla de destino** de la página **Asignaciones de columnas**.

## <a name="whats-next"></a>¿Qué sigue?  
 Después de seleccionar las tablas y vistas existentes que quiere copiar y de asignarlas a sus destinos, la página siguiente es **Guardar y ejecutar el paquete**. En esta página, especifique si quiere ejecutar la operación de copia inmediatamente. Según la configuración, también puede guardar el paquete de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] creado por el asistente para personalizarlo y volver a usarlo más adelante. Para más información, vea [Guardar y ejecutar paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
 ## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


