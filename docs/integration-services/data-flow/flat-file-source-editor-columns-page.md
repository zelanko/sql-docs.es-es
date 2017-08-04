---
title: "Editor de origen de archivo (página columnas) planos | Documentos de Microsoft"
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
- sql13.dts.designer.flatfilesourceadapter.columns.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: b5af5f65-c087-44fd-b5ae-d0441245fef2
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a34e304d72b80412f5527dcb75f00b6dcb2fcbb2
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="flat-file-source-editor-columns-page"></a>Editor de origen de archivos planos (página Columnas)
  Use el nodo **Columnas** del cuadro de diálogo **Editor de origen de archivos planos** para asignar una columna de salida a cada columna externa (origen).  
  
> [!NOTE]  
>  La propiedad **FileNameColumnName** del origen de archivo plano y la propiedad **FastParse** de sus columnas de salida no están disponibles en el **Editor de origen de archivos planos**, pero se puede establecer con el **Editor avanzado**. Para obtener más información acerca de estas propiedades, vea la sección sobre el origen de archivos planos en [Flat File Custom Properties](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
 Para obtener más información acerca del origen de archivo plano, vea [Flat File Source](../../integration-services/data-flow/flat-file-source.md).  
  
## <a name="options"></a>Opciones  
 **Columnas externas disponibles**  
 Muestra la lista de columnas externas disponibles en el origen de datos. Esta tabla no se puede usar para agregar o quitar columnas.  
  
 **Columna externa**  
 Vea las columnas externas (origen) en el orden en que la tarea las leerá. Puede cambiar este orden si elimina primero las columnas seleccionadas en la tabla y luego selecciona las columnas externas de la lista en un orden diferente.  
  
 **Columna de salida**  
 Permite proporcionar un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir un nombre único y descriptivo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origen de archivos planos &#40; Página Administrador de conexiones &#41;](../../integration-services/data-flow/flat-file-source-editor-connection-manager-page.md)   
 [Editor de origen de archivos planos &#40; Página de salida de error &#41;](../../integration-services/data-flow/flat-file-source-editor-error-output-page.md)   
 [Administrador de conexión de archivos planos](../../integration-services/connection-manager/flat-file-connection-manager.md)  
  
  
