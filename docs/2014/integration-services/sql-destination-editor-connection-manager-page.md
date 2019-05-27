---
title: Editor de destino de SQL (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdestadapter.connection.f1
helpviewer_keywords:
- SQL Server Destination Editor
ms.assetid: 423e1654-54af-47c6-ab6f-98670534557d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3bffc98a14c1a8bc672e9f15a4bad8b6f5a7dbe
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66055409"
---
# <a name="sql-destination-editor-connection-manager-page"></a>Editor de destino de SQL (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de SQL** para especificar la información de orígenes de datos y para obtener una vista previa de los resultados. El destino [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] carga los datos en tablas o vistas en una base de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Para obtener más información acerca del destino de SQL Server, vea [SQL Server Destination](data-flow/sql-server-destination.md).  
  
## <a name="options"></a>Opciones  
 **Administrador de conexiones OLE DB**  
 Seleccione una conexión existente de la lista o cree una nueva conexión haciendo clic en **Nueva**.  
  
 **Nueva**  
 Cree una conexión mediante el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
 **Usar una tabla o una vista**  
 Seleccione una tabla o vista existente de la lista, o cree una nueva conexión haciendo clic en **Nueva**.  
  
 **Nueva**  
 Permite crear una tabla con el cuadro de diálogo **Crear tabla** .  
  
> [!NOTE]  
>  Al hacer clic en **Nueva**, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] genera una instrucción predeterminada CREATE TABLE basada en el origen de datos conectado. La instrucción predeterminada CREATE TABLE no incluirá el atributo FILESTREAM, aunque la tabla de origen tenga una columna con el atributo FILESTREAM declarado. Para ejecutar un componente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] con el atributo FILESTREAM, implemente en primer lugar el almacenamiento de FILESTREAM en la base de datos de destino. A continuación, agregue el atributo FILESTREAM a la instrucción CREATE TABLE en el cuadro de diálogo **Crear tabla** . Para más información, vea [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Vista previa**  
 Obtenga una vista previa de los resultados mediante el cuadro de diálogo **Vista previa de los resultados de la consulta** . La vista previa puede mostrar hasta 200 filas.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de SQL &#40;página Asignaciones&#41;](../../2014/integration-services/sql-destination-editor-mappings-page.md)   
 [Editor de destino de SQL &#40;página Avanzadas&#41;](../../2014/integration-services/sql-destination-editor-advanced-page.md)   
 [Realizar una carga masiva de datos mediante el destino de SQL Server](data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  
