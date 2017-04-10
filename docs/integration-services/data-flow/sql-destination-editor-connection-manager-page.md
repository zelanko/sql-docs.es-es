---
title: "Editor de destino de SQL (p&#225;gina Administrador de conexiones) | Microsoft Docs"
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
  - "sql13.dts.designer.sqlserverdestadapter.connection.f1"
helpviewer_keywords: 
  - "Editor de destino de SQL Server"
ms.assetid: 423e1654-54af-47c6-ab6f-98670534557d
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# Editor de destino de SQL (p&#225;gina Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de SQL** para especificar la información de orígenes de datos y para obtener una vista previa de los resultados. El destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carga los datos en tablas o vistas en una base de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obtener más información acerca del destino de SQL Server, vea [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md).  
  
## Opciones  
 **OLE DB, administrador de conexiones**  
 Seleccione una conexión existente de la lista o cree una nueva conexión haciendo clic en **Nueva**.  
  
 **Nuevo**  
 Cree una nueva conexión mediante el cuadro de diálogo **Configurar el administrador de conexiones OLE DB**.  
  
 **Usar una tabla o una vista**  
 Seleccione una tabla o vista existente de la lista, o cree una nueva conexión haciendo clic en **Nueva**.  
  
 **Nuevo**  
 Cree una tabla nueva mediante el cuadro de diálogo **Crear tabla**.  
  
> [!NOTE]  
>  Al hacer clic en **Nueva**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera una instrucción predeterminada CREATE TABLE basada en el origen de datos conectado. La instrucción predeterminada CREATE TABLE no incluirá el atributo FILESTREAM, aunque la tabla de origen tenga una columna con el atributo FILESTREAM declarado. Para ejecutar un componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el atributo FILESTREAM, implemente en primer lugar el almacenamiento de FILESTREAM en la base de datos de destino. A continuación, agregue el atributo FILESTREAM a la instrucción CREATE TABLE en el cuadro de diálogo **Crear tabla** . Para obtener más información, vea [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Vista previa**  
 Obtenga una vista previa de los resultados mediante el cuadro de diálogo **Vista previa de los resultados de la consulta**. La vista previa puede mostrar hasta 200 filas.  
  
## Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de SQL &#40;página Asignaciones&#41;](../../integration-services/data-flow/sql-destination-editor-mappings-page.md)   
 [Editor de destino de SQL &#40;página Avanzadas&#41;](../../integration-services/data-flow/sql-destination-editor-advanced-page.md)   
 [Realizar una carga masiva de datos mediante el destino de SQL Server](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  