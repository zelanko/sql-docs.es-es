---
title: Editor de transformación script (página columnas de entrada) | Documentos de Microsoft
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
- sql12.dts.designer.scriptcomponent.inputcolumn.f1
helpviewer_keywords:
- Script Transformation Editor
ms.assetid: d6e4ce84-3335-48e6-82d3-1c359ed87f63
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 456f1abba1045da01c162dfb23738bcb989a9341
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111588"
---
# <a name="script-transformation-editor-input-columns-page"></a>Editor de transformación Script (página Columnas de entrada)
  Utilice la página **Columnas de entrada** del cuadro de diálogo **Editor de transformación Script** para definir las propiedades de las columnas de entrada.  
  
> [!NOTE]  
>  La página **Columnas de entrada** no se muestra para los componentes de origen, que tienen salidas, pero no entradas.  
  
 Para obtener más información acerca del componente de script, vea [Script Component](data-flow/transformations/script-component.md) y [Configuring the Script Component in the Script Component Editor](extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Para obtener información acerca de cómo programar el componente de script, vea [Extending the Data Flow with the Script Component](extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de entrada**  
 Seleccione las entradas disponibles de la lista.  
  
 **Columnas de entrada disponibles**  
 Mediante las casillas, indique las columnas que utilizarán la transformación de script.  
  
 **Columna de entrada**  
 Seleccione de la lista de entradas disponibles las columnas para cada fila. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles**.  
  
 **Alias de salida**  
 Escriba un alias para cada columna de salida. El nombre predeterminado es el de la columna de entrada, pero puede elegir cualquier nombre descriptivo único.  
  
 **Tipo de uso**  
 Especifique si la transformación de script tratará cada columna como `ReadOnly` o `ReadWrite`.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Seleccionar tipo de componente de Script](../../2014/integration-services/select-script-component-type.md)   
 [Editor de transformación script &#40;entradas y salidas de página&#41;](../../2014/integration-services/script-transformation-editor-inputs-and-outputs-page.md)   
 [Editor de transformación script &#40;página secuencia de comandos&#41;](../../2014/integration-services/script-transformation-editor-script-page.md)   
 [Editor de transformación script &#40;página Administradores de conexión&#41;](../../2014/integration-services/script-transformation-editor-connection-managers-page.md)   
 [Ejemplos de componente de script adicionales](extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)  
  
  