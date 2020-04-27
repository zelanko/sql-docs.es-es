---
title: Editor de origen de archivos planos (página columnas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfilesourceadapter.columns.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: b5af5f65-c087-44fd-b5ae-d0441245fef2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f8fda95b51f568098b0ac9fc13b8a204adb71c51
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66058611"
---
# <a name="flat-file-source-editor-columns-page"></a>Editor de origen de archivos planos (página Columnas)
  Use el nodo **Columnas** del cuadro de diálogo **Editor de origen de archivos planos** para asignar una columna de salida a cada columna externa (origen).  
  
> [!NOTE]  
>  La `FileNameColumnName` propiedad del origen de archivo plano y la `FastParse` propiedad de sus columnas de salida no están disponibles en el **Editor de origen de archivos planos**, pero se pueden establecer mediante el **editor avanzado**. Para obtener más información acerca de estas propiedades, vea la sección sobre el origen de archivos planos en [Flat File Custom Properties](data-flow/flat-file-custom-properties.md).  
  
 Para obtener más información acerca del origen de archivo plano, vea [Flat File Source](data-flow/flat-file-source.md).  
  
## <a name="options"></a>Opciones  
 **Columnas externas disponibles**  
 Muestra la lista de columnas externas disponibles en el origen de datos. Esta tabla no se puede usar para agregar o quitar columnas.  
  
 **Columna externa**  
 Vea las columnas externas (origen) en el orden en que la tarea las leerá. Puede cambiar este orden si elimina primero las columnas seleccionadas en la tabla y luego selecciona las columnas externas de la lista en un orden diferente.  
  
 **Columna de salida**  
 Permite proporcionar un nombre único para cada columna de salida. El nombre predeterminado es el nombre de la columna externa (origen) seleccionada; sin embargo, puede elegir un nombre único y descriptivo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origen de archivos planos &#40;página Administrador de conexiones&#41;](../../2014/integration-services/flat-file-source-editor-connection-manager-page.md)   
 [Editor de origen de archivos planos &#40;página salida de error&#41;](../../2014/integration-services/flat-file-source-editor-error-output-page.md)   
 [Administrador de conexiones de archivos planos](connection-manager/file-connection-manager.md)  
  
  
