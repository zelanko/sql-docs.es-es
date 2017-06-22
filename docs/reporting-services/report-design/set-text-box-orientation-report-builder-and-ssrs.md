---
title: "Establecer la orientación de cuadro de texto (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 64bd53f4-2f31-4732-8c2e-64c7b54b6972
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4cc52b4687f9a2c944ea3a93c15b637d894c7a96
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="set-text-box-orientation-report-builder-and-ssrs"></a>Establecer la orientación del cuadro de texto (Generador de informes y SSRS)
En un informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , puede girar un cuadro de texto en varias direcciones:   
* Horizontalmente   
* Verticalmente (se gira 90 grados y el texto se lee de arriba abajo)  
* Girar 270 grados (el texto lee de abajo arriba)   
  
Dado que se gira el cuadro de texto y no el texto, la rotación se aplica a todo el texto del cuadro de texto. No es posible especificar direcciones diferentes para las partes del texto. Debe establecer manualmente el ancho de columna y el alto de fila para alojar el texto girado.  
  
 La propiedad WritingMode, que se usa para especificar la orientación del texto, no se encuentra en el cuadro de diálogo **Propiedades de cuadro de texto** . Está en el panel de propiedades y debe establecer la propiedad en él.   
  
## <a name="to-rotate-text"></a>Para girar el texto  
  
1.  Cree un informe o abra uno existente y [agregue un cuadro de texto](../../reporting-services/report-design/add-move-or-delete-a-text-box-report-builder-and-ssrs.md) a la superficie de diseño.  
  
3.  Seleccione el cuadro de texto que quiera girar.  
  
2.  Si el panel de propiedades no está abierto, en la pestaña **Ver** active la casilla **Propiedades** .  
  
4.  En el panel de propiedades, busque la propiedad WritingMode y seleccione la orientación del texto que quiera aplicar al cuadro de texto.  
  
    > [!NOTE]  
    >  Cuando las propiedades del panel de propiedades se organizan en categorías, WritingMode está en la categoría **Localización** .  
  
5.  En el cuadro de lista, seleccione **Horizontal**, **Vertical**o **Rotate270**.  
  
## <a name="see-also"></a>Vea también  
 [Cuadros de texto &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/text-boxes-report-builder-and-ssrs.md)   
 [Tutorial: Dar formato a texto &#40;Generador de informes&#41;](../../reporting-services/tutorial-format-text-report-builder.md)  
  
  
