---
title: Cuadro de diálogo visibilidad de fila | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.rowvisibility.f1
- "10126"
ms.assetid: 557ecf70-62b1-47f5-9322-0ebdc809d018
caps.latest.revision: 12
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: aac18834e0fffce98ed0f0de508c019a737f6b0a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200765"
---
# <a name="row-visibility-dialog-box"></a>Cuadro de diálogo Visibilidad de fila
  Use el cuadro de diálogo **Visibilidad de fila** para mostrar u ocultar la fila seleccionada cuando se ejecuta el informe por primera vez o para usar otro elemento de informe para activar o desactivar la visibilidad de la fila.  
  
## <a name="options"></a>Opciones  
 **Cuando se ejecute inicialmente el informe**  
 Seleccione una opción para indicar cómo se muestra el elemento de informe inicialmente en el informe.  
  
 **Mostrar**  
 Seleccione esta opción para mostrar el elemento de informe.  
  
 **Ocultar**  
 Seleccione esta opción para ocultar el elemento de informe.  
  
 **Mostrar u ocultar en función de una expresión**  
 Seleccione esta opción para modificar la visibilidad inicial por medio de una expresión.  
  
 Escriba una expresión que se evalúa como un `Boolean` valor `True` para ocultar el elemento y `False` para mostrar el elemento. Haga clic en el botón Expresión (**fx**) para editar la expresión.  
  
 **Este elemento de informe puede alternar la presentación**  
 Elija esta opción para mostrar una imagen de alternancia que permita que el usuario muestre u oculte este elemento de informe en un visor de informes HTML.  
  
 Escriba o seleccione el nombre de un cuadro de texto del informe en el que aparezca una imagen de alternancia, por ejemplo, Textbox1. El cuadro de texto que elija debe estar en el ámbito actual o en el ámbito contenedor de este elemento de informe. Por ejemplo, para alternar la visibilidad de las filas asociadas a un grupo secundario, seleccione un cuadro de texto de una fila asociada al grupo primario. Para alternar la visibilidad de un gráfico, seleccione un cuadro de texto que esté en el mismo ámbito contenedor que el gráfico; por ejemplo, un rectángulo o el cuerpo del informe.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Agregar una acción de expandir y contraer a un elemento &#40;Generador de informes y SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Imágenes &#40;generador de informes y SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Diseñador de informes (Ayuda F1)](tools/report-designer-f1-help.md)  
  
  
