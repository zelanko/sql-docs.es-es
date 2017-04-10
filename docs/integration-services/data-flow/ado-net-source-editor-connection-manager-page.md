---
title: "Editor de or&#237;genes de ADO NET (p&#225;gina Administrador de conexiones) | Microsoft Docs"
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
  - "sql13.dts.designer.adonetsource.connection.f1"
ms.assetid: 7de3f438-bdd6-49b5-937a-47369e754943
caps.latest.revision: 19
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 19
---
# Editor de or&#237;genes de ADO NET (p&#225;gina Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de orígenes de ADO NET** para seleccionar el administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para el origen. Esta página también permite seleccionar una tabla o vista de la base de datos.  
  
 Para obtener más información acerca del origen de ADO NET, vea [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Para abrir la página Administrador de conexiones**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tiene el origen de ADO NET.  
  
2.  En la pestaña **Flujo de datos**, haga doble clic en el origen de ADO NET.  
  
3.  En el **Editor de orígenes de ADO NET**, haga clic en **Administrador de conexiones**.  
  
## Opciones estáticas  
 **Administrador de conexiones de ADO.NET**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nuevo**  
 Cree un nuevo administrador de conexiones mediante el cuadro de diálogo **Configurar el administrador de conexiones de ADO.NET**.  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Description|  
|------------|-----------------|  
|Tabla o vista|Recupera datos de una tabla o vista del origen de datos [!INCLUDE[vstecado](../../includes/vstecado-md.md)] .|  
|Comando SQL|Recupera datos del origen de datos [!INCLUDE[vstecado](../../includes/vstecado-md.md)] mediante una consulta SQL.|  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos**. **Vista previa** puede mostrar hasta 200 filas.  
  
> [!NOTE]  
>  Cuando genera una vista previa de datos, las columnas con un tipo definido por el usuario CLR no contienen datos. En su lugar, se muestran los valores \<valor demasiado grande; no se mostrará> o System.Byte[]. El primero se muestra cuando se tiene acceso al origen de datos mediante el proveedor [!INCLUDE[vstecado](../../includes/vstecado-md.md)] y el último, cuando se utiliza el proveedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## Opciones dinámicas del modo de acceso a datos  
  
### Modo de acceso a datos = Tabla o vista  
 **Nombre de la tabla o la vista**  
 Seleccione el nombre de la tabla o vista de los disponibles en una lista del origen de datos.  
  
### Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien busque el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
 **Generar consulta**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para encontrar el archivo que contiene el texto de la consulta SQL.  
  
## Vea también  
 [Editor de orígenes de ADO NET &#40;página Columnas&#41;](../../integration-services/data-flow/ado-net-source-editor-columns-page.md)   
 [Editor de orígenes de ADO NET &#40;página Salida de error&#41;](../../integration-services/data-flow/ado-net-source-editor-error-output-page.md)   
 [Administrador de conexiones ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)  
  
  