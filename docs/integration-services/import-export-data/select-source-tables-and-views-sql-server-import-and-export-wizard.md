---
title: Seleccionar tablas de origen y vistas (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
caps.latest.revision: 96
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9a0c3c4fc8d41206ea077498dafb755e7b433a78
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Seleccionar tablas y vistas de origen (Asistente para importación y exportación de SQL Server)
  Después de especificar que quiere copiar una tabla completa o después de proporcionar una consulta, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Seleccionar tablas y vistas de origen**. En esta página, seleccione las tablas y vistas que quiera copiar. A continuación, asigne las tablas de origen a las tablas de destino nuevas o existentes. Opcionalmente, revise la asignación de columnas individuales y obtenga una vista previa de los datos de ejemplo.

> [!TIP]
> Si tiene que copiar más de una base de datos de SQL Server u objetos de base de datos de SQL Server que no sean tablas y vistas, use el Asistente para la base de datos de copia en lugar de la importación y el Asistente para exportación. Para más información, vea [Usar el Asistente para copiar bases de datos](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>Captura de pantalla: si va a copiar tablas  
 La captura de pantalla siguiente muestra un ejemplo de la **seleccionar tablas de origen y vistas** página del asistente si seleccionó previamente la **copiar los datos de una o más tablas o vistas** opción el ** Especificar copia de tabla o consulta** página. En la lista, se ven todas las tablas y vistas disponibles del origen de datos.
 
En este ejemplo, el **origen** lista contiene todas las tablas de la base de datos de ejemplo AdventureWorks. La fila seleccionada se muestra que el usuario desea copiar el **Sales.Customer** tabla desde el origen a la nueva **Sales.CustomerNew** tabla en el destino. 
   
 ![Página Seleccionar las tablas de la importación y el Asistente para exportación de](../../integration-services/import-export-data/media/select-tables1.png "página Seleccionar las tablas de la importación y el Asistente para exportación")
  
## <a name="screen-shot---if-you-provided-a-query"></a>Captura de pantalla: si se proporciona una consulta  
 La captura de pantalla siguiente muestra un ejemplo de la **seleccionar tablas de origen y vistas** página del asistente si seleccionó previamente la **escribir una consulta para especificar los datos que se va a transferir** opción en el **Especificar copia de tabla o consulta** página. El **origen** lista contiene solo una sola fila, donde el elemento denominado `[Query]` representa la consulta que proporciona en el **proporcionar una consulta de origen** página.
 
En este ejemplo, el usuario quiere copiar los resultados de la consulta del origen en la tabla **Sales.CustomerNew** del destino.  
    
 ![Página Seleccionar las tablas de la importación y el Asistente para exportación de](../../integration-services/import-export-data/media/select-tables2.png "página Seleccionar las tablas de la importación y el Asistente para exportación")  

## <a name="select-source-and-destination-tables"></a>Seleccionar tablas de destino y origen 
**Origen**  
Utilice las casillas para seleccionar en la lista las tablas y vistas disponibles que deben copiarse en el destino. De forma predeterminada, los datos del origen de datos se copian sin cambios. Si crea una nueva tabla de destino, el esquema para la nueva tabla: es decir, la lista de columnas y sus propiedades - también se copia sin cambios desde el origen de datos.

Si se proporciona una consulta, la lista contiene solo un elemento con el nombre `[Query]`. 

**Destino**  
 Seleccione una tabla de destino de la lista para cada tabla o consulta de origen, o escriba el nombre de una nueva tabla que quiera que cree el asistente. Si selecciona una tabla de destino existente, esta debe tener columnas con tipos de datos que sean compatibles con los datos de origen.  

> [!NOTE]
> Si detiene el asistente en este punto para crear una tabla de forma manual en la base de datos de destino con una herramienta externa (como  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]), la nueva tabla no será visible de forma inmediata en la lista de tablas de destino disponibles. Para actualizar la lista de tablas de destino, retroceda hasta la página **Seleccionar un destino** , vuelva a seleccionar la base de datos de destino para actualizar la lista de tablas y vistas disponibles y luego regrese a la página **Seleccionar tablas y vistas de origen** .  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Opcionalmente, revise las asignaciones de columna y obtener una vista previa de datos
**Editar asignaciones**   
Si lo desea, haga clic en **editar asignaciones** para mostrar la **asignaciones de columnas** cuadro de diálogo para la tabla seleccionada. Use el cuadro de diálogo **Asignaciones de columnas** para hacer lo siguiente:
-   Revise la asignación de columnas individuales entre el origen y el destino.
-   Copie solo un subconjunto de columnas si selecciona **Omitir** para las columnas que no desea copiar.

Para más información, vea [Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Vista previa**  
Si lo desea, haga clic en **vista previa** para obtener una vista previa de hasta 200 filas de datos de ejemplo en el **vista previa de datos** cuadro de diálogo. Esto confirma que el asistente va a copiar los datos que quiere copiar. Para más información, vea [Vista previa de los datos](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
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

**Tipos de datos en los libros de Excel**. Excel no es una base de datos típica. Sus columnas no tienen tipos de datos fijos. El asistente solo reconoce un conjunto limitado de tipos de datos en Excel: numérico, moneda, booleano, fecha y hora, cadena (255 caracteres o menos) y memorando (más de 255 caracteres). El Asistente prueba un cierto número de filas (de forma predeterminada, las ocho primeras filas) en un origen de datos de Excel existente para elegir el tipo de datos de cada columna.

Cuando el asistente tiene que realizar conversiones de tipo de datos explícitas para cargar desde Excel o en Excel, normalmente se muestra la página **Revisar asignación de tipos de datos** donde puede revisar esas conversiones. Entre estas conversiones, se pueden incluir las siguientes.
-   Conversión entre columnas numéricas de Excel de doble precisión y columnas numéricas de otros tipos.
-   Conversión entre columnas de cadena de Excel de 255 caracteres y columnas de cadena de diferentes longitudes.
-   Conversión entre columnas de cadena de Unicode Excel y columnas de cadena no Unicode que utilizan páginas de códigos específicas.

### <a name="special-considerations-for-excel-sources"></a>Consideraciones especiales para orígenes de Excel
**Valores nulos o que faltan en datos importados**. Cuando una columna de Excel parece contener varios tipos de datos en las ocho primeras filas muestreadas por el asistente: por ejemplo, combinados valores numéricos con valores de texto - el asistente elige el tipo como el tipo de datos de la columna y devuelve valores null en las celdas que |expresiónn datos de otros tipos. No hay ninguna forma de cambiar este comportamiento del asistente.

**Cadenas truncadas en datos importados**. Cuando el asistente determina que una columna de Excel contiene datos de texto, el asistente selecciona el tipo de datos de la columna (cadena o memorando) en función del valor más largo que muestrea en las primeras ocho filas. Si el asistente no encuentra valores de más de 255 caracteres en las filas que muestrea, trata a la columna como una columna de cadenas de 255 caracteres en lugar de una columna de memorando y trunca los valores de más de 255 caracteres. Para importar datos de una columna memorando sin que se trunquen, tiene que asegurarse de que la columna de memorando contiene al menos un valor de más de 255 caracteres en las ocho primeras filas muestreadas por el asistente.

### <a name="special-considerations-for-excel-destinations"></a>Consideraciones especiales para destinos de Excel
**Especificar un rango existente**. Cuando se especifica un rango existente como el destino, recibirá un error si el intervalo tiene menos *columnas* que los datos de origen. Sin embargo, si el intervalo que especifique tiene menos *filas* que los datos de origen, el asistente sigue escribiendo filas y extiende la definición del intervalo para que coincida con el nuevo número de filas.

**Guardar datos de memorando (ntext)**. Para poder guardar correctamente cadenas de más de 255 caracteres en una columna de Excel, el asistente debe reconocer el tipo de datos de la columna de destino como **memorando** y no como **cadena**.
-   Si la tabla de destino ya contiene filas de datos, las ocho primeras filas que pruebe el asistente tienen que contener al menos una fila con un valor de más de 255 caracteres en la columna de memorando.
-   Si la tabla de destino se crea con el asistente, el **CREATE TABLE** debe usar la instrucción **LONGTEXT** (o uno de sus sinónimos) como el tipo de datos de la la columna de memorando. Compruebe el **CREATE TABLE** instrucción y revisar, si es necesario, haciendo clic en **Editar SQL** junto a la **crear tabla de destino** opción en la **columna Asignaciones de** página.

## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de seleccionar las tablas y vistas existentes que quiere copiar y de asignarlas a sus destinos, la página siguiente es **Guardar y ejecutar el paquete**. En esta página, especifique si quiere ejecutar la operación de copia inmediatamente. Según la configuración, también puede guardar el paquete de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] creado por el asistente para personalizarlo y volver a usarlo más adelante. Para más información, vea [Guardar y ejecutar paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
 ## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



