---
title: Editor de origen de archivo (página columnas) planos | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.flatfilesourceadapter.columns.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: b5af5f65-c087-44fd-b5ae-d0441245fef2
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3be667dc6fe7dcaefdc183a831f762a566a56c99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111597"
---
# <a name="flat-file-source-editor-columns-page"></a>Editor de origen de archivos planos (página Columnas)
  Use el nodo **Columnas** del cuadro de diálogo **Editor de origen de archivos planos** para asignar una columna de salida a cada columna externa (origen).  
  
> [!NOTE]  
>  El `FileNameColumnName` propiedad del origen de archivo sin formato y la `FastParse` propiedad de sus columnas de salida no están disponibles en la **Editor de origen de archivos planos**, pero se puede establecer mediante el uso de la **Editor avanzado** . Para obtener más información acerca de estas propiedades, vea la sección sobre el origen de archivos planos en [Flat File Custom Properties](data-flow/flat-file-custom-properties.md).  
  
 Para obtener más información acerca del origen de archivo plano, vea [Flat File Source](data-flow/flat-file-source.md).  
  
## <a name="options"></a>Opciones  
 **Columnas externas disponibles**  
 Muestra la lista de columnas externas disponibles en el origen de datos. Esta tabla no se puede usar para agregar o quitar columnas.  
  
 **Columna externa**  
 Vea las columnas externas (origen) en el orden en que la tarea las leerá. Puede cambiar este orden si elimina primero las columnas seleccionadas en la tabla y luego selecciona las columnas externas de la lista en un orden diferente.  
  
 **Columna de salida**  
 Permite proporcionar un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir un nombre único y descriptivo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origen de archivos planos &#40;página Administrador de conexiones&#41;](../../2014/integration-services/flat-file-source-editor-connection-manager-page.md)   
 [Editor de origen de archivos planos &#40;página de salida de Error&#41;](../../2014/integration-services/flat-file-source-editor-error-output-page.md)   
 [Administrador de conexiones de archivos planos](connection-manager/file-connection-manager.md)  
  
  