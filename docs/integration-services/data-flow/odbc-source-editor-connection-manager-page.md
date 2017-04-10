---
title: "Editor de origen de ODBC (p&#225;gina Administrador de conexiones) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.odbcsource.connection.f1"
ms.assetid: e2c8dc83-6394-4d6c-9232-97e94be72431
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Editor de origen de ODBC (p&#225;gina Administrador de conexiones)
  Use la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de ODBC** para seleccionar el administrador de conexiones de ODBC para el origen. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
 Para obtener más información acerca del origen de ODBC, vea [ODBC Source](../../integration-services/data-flow/odbc-source.md).  
  
## Lista de tareas  
 **Para abrir la página Administrador de conexiones del Editor de origen de ODBC**  
  
-   En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tiene el origen de ODBC.  
  
-   En la pestaña **Flujo de datos**, haga doble clic en el origen de ODBC.  
  
## Opciones  
  
### Administrador de conexiones  
 Seleccione un administrador de conexiones de ODBC existente en la lista o haga clic en **Nueva** para crear una nueva conexión. La conexión puede ser a cualquier base de datos compatible con ODBC.  
  
### Nuevo  
 Haga clic en **Nueva**. Se abrirá el cuadro de diálogo **Configurar el administrador de conexiones ODBC** , donde puede crear un administrador de conexiones ODBC nuevo.  
  
### Modo de acceso a datos  
 Elija el método para la selección de datos desde el origen. Las opciones se muestran en la tabla siguiente:  
  
|Opción|Description|  
|------------|-----------------|  
|Nombre de tabla|Recupera datos de una tabla o vista del origen de datos de ODBC. Cuando seleccione esta opción, seleccione un valor de la lista para lo siguiente:|  
||**Nombre de la tabla o la vista**: seleccione una tabla o vista disponible en la lista o escriba una expresión regular para identificar la tabla.|  
||Esta lista contiene solo las 1000 primeras tablas. Si la base de datos contiene más de 1000 tablas, puede escribir el principio de un nombre de tabla o usar el comodín (*) para escribir cualquier parte del nombre con el fin de mostrar la tabla o las tablas que desea usar.|  
|Comando SQL|Recupera datos del origen de datos de ODBC mediante una consulta SQL. Debe escribir la consulta con la sintaxis de la base de datos de origen con la que está trabajando. Cuando seleccione esta opción, escriba una consulta de una de las siguientes maneras:|  
||Escriba el texto de la consulta SQL en el campo de **Texto de comando SQL** .|  
||Haga clic en **Examinar** para cargar la consulta SQL desde un archivo de texto.|  
||Haga clic en **Analizar consulta** para comprobar la sintaxis del texto de la consulta.|  
  
### Vista previa  
 Haga clic en **Vista previa** para ver hasta las 200 primeras filas de los datos extraídos de la tabla o la vista seleccionada.  
  
## Vea también  
 [Propiedades personalizadas del origen ODBC](../../integration-services/data-flow/odbc-source-custom-properties.md)   
 [Editor de orígenes ODBC &#40;página Columnas&#41;](../../integration-services/data-flow/odbc-source-editor-columns-page.md)   
 [Editor de orígenes ODBC &#40;página Salida de error&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
  