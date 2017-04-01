---
title: "Editor de origen de Excel (p&#225;gina Administrador de conexiones) | Microsoft Docs"
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
  - "sql13.dts.designer.excelsourceadapter.connection.f1"
helpviewer_keywords: 
  - "Editor de origen de Excel"
ms.assetid: 428e04e0-ad98-45d0-8345-12ec1b67b2eb
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# Editor de origen de Excel (p&#225;gina Administrador de conexiones)
  Utilice el nodo **Administrador de conexiones** del cuadro de diálogo **Editor de origen de Excel** para seleccionar el libro de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] que utilizará el origen. El origen de Excel lee los datos de una hoja de cálculo o un rango con nombre de un libro existente.  
  
> [!NOTE]  
>  La propiedad **CommandTimeout** del origen de Excel no está disponible en el **Editor de origen de Excel**, pero se puede establecer mediante el **Editor avanzado**. Para obtener más información acerca de esta propiedad, vea la sección Origen de Excel de [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
 Para obtener más información acerca del origen de Excel, vea [Excel Source](../../integration-services/data-flow/excel-source.md).  
  
## Opciones estáticas  
 **OLE DB, administrador de conexiones**  
 Seleccione un administrador de conexiones de Excel en la lista o cree una nueva conexión haciendo clic en **Nuevo**.  
  
 **Nuevo**  
 Cree un nuevo administrador de conexiones mediante el cuadro de diálogo **Administrador de conexiones con Excel**.  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Value|Description|  
|-----------|-----------------|  
|Tabla o vista|Recupera los datos de una hoja de cálculo o un rango con nombre del archivo Excel.|  
|Variable de nombre de tabla o nombre de vista|Especifique la hoja de calculo o el rango con nombre de una variable.<br /><br /> **Información relacionada**: [Usar variables en paquetes](../Topic/Use%20Variables%20in%20Packages.md)|  
|Comando SQL|Recupera datos del archivo Excel mediante una consulta SQL. Para obtener información acerca de la sintaxis de consultas, vea [Excel Source](../../integration-services/data-flow/excel-source.md).|  
|Comando SQL de variable|Especifique el texto de la consulta SQL de una variable.|  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos**. La vista previa puede mostrar hasta 200 filas.  
  
## Opciones dinámicas del modo de acceso a datos  
  
### Modo de acceso a datos = Tabla o vista  
 **Nombre de la hoja de Excel**  
 Seleccione el nombre de la hoja de cálculo o el rango con nombre de los disponibles en el libro de Excel.  
  
### Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la hoja de cálculo o el rango con nombre.  
  
### Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien examine el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
 **Parámetros**  
 Si ha escrito una consulta con parámetros mediante ? como marcador de posición de parámetro en el texto de la consulta, utilice el cuadro de diálogo **Establecer parámetros de consulta** para asignar los parámetros de entrada de las consultas a las variables del paquete.  
  
 **Generar consulta**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para encontrar el archivo que contiene el texto de la consulta SQL.  
  
 **Analizar consulta**  
 Comprueba la sintaxis del texto de la consulta.  
  
### Modo de acceso a datos = Comando SQL de variable  
 **Nombre de variable**  
 Seleccione la variable que contiene el texto de la consulta SQL.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origen de Excel &#40;página Columnas&#41;](../../integration-services/data-flow/excel-source-editor-columns-page.md)   
 [Editor de origen de Excel &#40;página Salida de error&#41;](../../integration-services/data-flow/excel-source-editor-error-output-page.md)   
 [Administrador de conexiones con Excel](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  