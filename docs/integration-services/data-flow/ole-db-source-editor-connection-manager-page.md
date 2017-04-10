---
title: "Editor de origen de OLE DB (p&#225;gina Administrador de conexiones) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.oledbsourceadapter.connection.f1"
helpviewer_keywords: 
  - "origen de OLE DB, editor de"
ms.assetid: 53699902-8699-4547-b56b-a5b2079e98b6
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 42
---
# Editor de origen de OLE DB (p&#225;gina Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de OLE DB** para seleccionar el administrador de conexiones OLE DB para el origen. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
> [!NOTE]  
>  Para cargar datos desde un origen de datos que use [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, use un origen de OLE DB. No puede usar un origen de Excel para cargar datos desde un origen de datos de Excel 2007. Para más información, consulte [Configure OLE DB Connection Manager](../../integration-services/connection-manager/configure-ole-db-connection-manager.md).  
>   
>  Para cargar datos desde un origen de datos que use [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 o anterior, use un origen de Excel. Para más información, vea [Editor de origen de Excel &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md).  
  
> [!NOTE]  
>  La propiedad **CommandTimeout** del origen de OLE DB no está disponible en el **Editor de origen de OLE DB**, pero se puede establecer mediante el **Editor avanzado**. Para obtener más información acerca de esta propiedad, vea la sección Origen de Excel de [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
 Para obtener más información acerca del origen de OLE DB, vea [OLE DB Source](../../integration-services/data-flow/ole-db-source.md).  
  
## Abrir el Editor de origen de OLE DB (página Administrador de conexiones)  
  
1.  Agregue el origen de OLE DB al paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en el componente de origen y, después, haga clic en **Editar**.  
  
3.  Haga clic en **Administrador de conexiones**.  
  
## Opciones estáticas  
 **OLE DB, administrador de conexiones**  
 Seleccione un administrador de conexiones de la lista o haga clic en **Nuevo** para crear una conexión.  
  
 **Nuevo**  
 Cree un administrador de conexiones con el cuadro de diálogo **Configurar el administrador de conexiones OLE DB**.  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Description|  
|------------|-----------------|  
|Tabla o vista|Obtenga datos de una tabla o vista en el origen de datos OLE DB.|  
|Variable de nombre de tabla o nombre de vista|Especifique el nombre de la tabla o vista de una variable.<br /><br /> **Información relacionada:** [Usar variables en paquetes](../Topic/Use%20Variables%20in%20Packages.md)|  
|Comando SQL|Obtenga datos del origen de datos OLE DB mediante una consulta SQL.|  
|Comando SQL de variable|Especifique el texto de la consulta SQL de una variable.|  
  
 **Vista previa**  
 Muestra una vista previa de los resultados con el cuadro de diálogo **Vista de datos**. **Vista previa** puede mostrar hasta 200 filas.  
  
> [!NOTE]  
>  Cuando genera una vista previa de datos, las columnas con un tipo definido por el usuario CLR no contienen datos. En su lugar, se muestran los valores \<valor demasiado grande; no se mostrará> o System.Byte[]. El primero se muestra cuando se tiene acceso al origen de datos mediante el proveedor SQL OLE DB y el último, cuando se utiliza el proveedor Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## Opciones dinámicas del modo de acceso a datos  
  
### Modo de acceso a datos = Tabla o vista  
 **Nombre de la tabla o la vista**  
 Seleccione el nombre de la tabla o vista de los disponibles en una lista del origen de datos.  
  
### Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la tabla o vista.  
  
### Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, haga clic en **Generar consulta** para generar la consulta, o bien haga clic en **Examinar** para buscar el archivo que contiene el texto de la consulta.  
  
 **Parámetros**  
 Si ha escrito una consulta con parámetros mediante ? como marcador de posición de parámetro en el texto de la consulta, utilice el cuadro de diálogo **Establecer parámetros de consulta** para asignar los parámetros de entrada de las consultas a las variables del paquete.  
  
 **Generar consulta**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo que contiene el texto de la consulta SQL.  
  
 **Analizar consulta**  
 Comprueba la sintaxis del texto de la consulta.  
  
### Modo de acceso a datos = Comando SQL de variable  
 **Nombre de variable**  
 Seleccione la variable que contiene el texto de la consulta SQL.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origen de OLE DB &#40;página Columnas&#41;](../../integration-services/data-flow/ole-db-source-editor-columns-page.md)   
 [Editor de origen de OLE DB &#40;página Salida de error&#41;](../../integration-services/data-flow/ole-db-source-editor-error-output-page.md)   
 [Extraer datos mediante el origen de OLE DB](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)   
 [Administrador de conexiones OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
  