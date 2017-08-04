---
title: "Editor de destino de SQL (página avanzadas) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sqlserverdestadapter.advanced.f1
helpviewer_keywords:
- SQL Server Destination Editor
ms.assetid: 9b46bcf8-ddaf-4d7d-90a6-80bc19517e9b
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e279b5bc6ff340323647d1a93daeb006ec4c3cbf
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="sql-destination-editor-advanced-page"></a>Editor de destino de SQL (página Avanzadas)
  Utilice la página **Avanzadas** del cuadro de diálogo **Editor de destino de SQL** para especificar opciones avanzadas de inserción masiva.  
  
 Para obtener más información acerca del destino de SQL Server, vea [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md).  
  
## <a name="options"></a>Opciones  
 **Mantener valores de identidad**  
 Especifique si la tarea debe insertar valores en columnas de identidad. El valor predeterminado de esta propiedad es **False**.  
  
 **Mantener valores NULL**  
 Especifique si la tarea debe mantener valores NULL. El valor predeterminado de esta propiedad es **False**.  
  
 **Bloqueo de tabla**  
 Especifique si la tabla está bloqueada cuando se cargan los datos. El valor predeterminado de esta propiedad es **True**.  
  
 **Restricciones CHECK**  
 Especifique si la tarea debe comprobar restricciones. El valor predeterminado de esta propiedad es **True**.  
  
 **Activar desencadenadores**  
 Especifique si la inserción masiva debe activar desencadenadores en tablas. El valor predeterminado de esta propiedad es **False**.  
  
 **Primera fila**  
 Especifique la primera fila donde se va a insertar. El valor predeterminado de esta propiedad es **-1**, que indica que no se ha asignado ningún valor.  
  
> [!NOTE]  
>  Borre el cuadro de texto del **Editor de destino de SQL** para indicar que no desea asignar un valor a esta propiedad. Use -1 en la ventana **Propiedades** , el **Editor avanzado**y el modelo de objetos.  
  
 **Última fila**  
 Especifique la última fila donde se va a insertar. El valor predeterminado de esta propiedad es **-1**, que indica que no se ha asignado ningún valor.  
  
> [!NOTE]  
>  Borre el cuadro de texto del **Editor de destino de SQL** para indicar que no desea asignar un valor a esta propiedad. Use -1 en la ventana **Propiedades** , el **Editor avanzado**y el modelo de objetos.  
  
 **Número máximo de errores**  
 Especifique el número de errores que se pueden producir antes de que se detenga la inserción masiva. El valor predeterminado de esta propiedad es **-1**, que indica que no se ha asignado ningún valor.  
  
> [!NOTE]  
>  Borre el cuadro de texto del **Editor de destino de SQL** para indicar que no desea asignar un valor a esta propiedad. Use -1 en la ventana **Propiedades** , el **Editor avanzado**y el modelo de objetos.  
  
 **Timeout**  
 Especifique el número de segundos que se debe esperar antes de que la inserción masiva se detenga debido a un tiempo de espera.  
  
 **Columnas de orden**  
 Escriba los nombres de las columnas de orden. Las columnas se pueden ordenar en sentido ascendente o descendente. Si utiliza varias columnas de orden, delimite la lista con comas.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de SQL &#40; Página Administrador de conexiones &#41;](../../integration-services/data-flow/sql-destination-editor-connection-manager-page.md)   
 [Editor de destino de SQL &#40; Página Asignaciones &#41;](../../integration-services/data-flow/sql-destination-editor-mappings-page.md)   
 [Carga masiva de datos mediante el destino de SQL Server](../../integration-services/data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  
