---
title: Editor de origen de archivo (página Administrador de conexiones) planos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.flatfilesourceadapter.connection.f1
helpviewer_keywords:
- Flat File Source Editor
ms.assetid: 2efd6baa-ed75-4f3f-b667-514024cebdb8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3c729faa93cf445e7e0aff46fa94258bc7ea7a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058689"
---
# <a name="flat-file-source-editor-connection-manager-page"></a>Editor de origen de archivos planos (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de archivos planos** para seleccionar el administrador de conexiones que utilizará el origen de archivos planos. El origen de archivos planos lee los datos de un archivo de texto, que pueden estar en formato delimitado, tener un ancho fijo o ser mixtos.  
  
 Un origen de archivos planos puede utilizar uno de los siguientes tipos de administradores de conexiones:  
  
-   Un administrador de conexiones de archivos planos, si el origen es un único archivo plano. Para más información, consulte [Flat File Connection Manager](connection-manager/file-connection-manager.md).  
  
-   Un administrador de conexiones de varios archivos planos, si el origen son varios archivos planos y la tarea Flujo de datos se encuentra en un contenedor de bucles, como el contenedor de bucles For. En cada bucle del contenedor, el origen de archivos planos carga los datos del siguiente nombre de archivo que proporciona el administrador de conexiones de varios archivos planos. Para más información, consulte [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md).  
  
 Para obtener más información acerca del origen de archivo plano, vea [Flat File Source](data-flow/flat-file-source.md).  
  
## <a name="options"></a>Opciones  
 **Flat file connection manager**  
 Seleccione un administrador de conexiones de la lista o cree un nuevo administrador de conexiones haciendo clic en **Nuevo**.  
  
 **Nueva**  
 Crea un nuevo administrador de conexiones mediante el cuadro de diálogo **Editor del administrador de conexiones de archivos planos** .  
  
 **Conservar los valores null del origen como valores null en el flujo de datos**  
 Especifica si deben mantenerse los valores NULL cuando se extraen los datos. El valor predeterminado de esta propiedad es **false**. Cuando este valor es f`alse`, el origen de archivos planos reemplaza los valores NULL del origen de datos por los valores predeterminados correspondientes para cada columna, como cadenas vacías para las columnas de cadenas o cero para las columnas numéricas.  
  
 **Vista previa**  
 Muestra una vista previa de los resultados mediante el cuadro de diálogo **Vista de datos** . La vista previa puede mostrar hasta 200 filas.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de origen de archivos planos &#40;página Columnas&#41;](../../2014/integration-services/flat-file-source-editor-columns-page.md)   
 [Editor de origen de archivos planos &#40;página Salida de error&#41;](../../2014/integration-services/flat-file-source-editor-error-output-page.md)   
 [Administrador de conexiones de archivos planos](connection-manager/file-connection-manager.md)  
  
  
