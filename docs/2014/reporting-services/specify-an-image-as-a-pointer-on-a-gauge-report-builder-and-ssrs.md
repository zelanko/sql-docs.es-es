---
title: Especificar una imagen como un puntero en un medidor (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9d73b3c3-a068-4868-a2be-0cd261b6e92b
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: bce410684b433d8a444d36affa91f8134673432d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203788"
---
# <a name="specify-an-image-as-a-pointer-on-a-gauge-report-builder-and-ssrs"></a>Especificar una imagen como puntero en un medidor (Generador de informes y SSRS)
  El medidor contiene tres estilos integrados que se pueden usar para personalizar la apariencia del puntero. En el caso de un medidor radial, los estilos integrados son: aguja, marcador y barra. En el caso de un medidor lineal, los estilos integrados son: marcador, barra y termómetro. Si se requiere un puntero único, el usuario puede crear y especificar una imagen que se puede usar como un puntero totalmente funcional.  
  
 Cuando se especifica una imagen para el puntero, dicha imagen debe tener las especificaciones siguientes:  
  
-   El origen del puntero, o centro de giro, debe estar en la parte superior de la imagen.  
  
-   El final del puntero debe apuntar hacia abajo.  
  
 Puesto que el puntero tiene forma irregular, deberá especificar un color de transparencia para ocultar las partes innecesarias de la imagen. Considere la posibilidad de usar un color que no se mostraría normalmente en el medidor como color de transparencia, ya que los colores especificados no aparecerán en el medidor.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-an-image-as-a-pointer-on-the-gauge"></a>Especificar una imagen como un puntero en el medidor  
  
1.  En la vista Diseño, haga clic en el puntero del medidor.  
  
2.  (Opcional) Si no existe ningún puntero en el medidor, haga doble clic en el medidor y seleccione **agregar puntero**. Se agregará un puntero al medidor.  
  
3.  Haga clic en el **insertar** pestaña en la cinta de opciones y haga doble clic en el icono de imagen. Se abrirá el cuadro de diálogo **Propiedades de la imagen**.  
  
4.  Agregue una imagen al informe. Para obtener más información, consulte [incrustar una imagen en un informe &#40;el generador de informes y SSRS&#41;](report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md).  
  
5.  Abra el panel de propiedades.  
  
6.  En la superficie de diseño, haga clic en el puntero. Las propiedades del puntero se muestran en el panel de propiedades.  
  
7.  Expanda el nodo PointerImage.  
  
8.  En **origen**, seleccione **incrustada** en la lista desplegable.  
  
    > [!NOTE]  
    >  Si la imagen está almacenada en la base de datos o en Internet, puede especificar la opción adecuada para esta propiedad. Para obtener más información, consulte [cuadro de diálogo de propiedades de imagen, General &#40;el generador de informes y SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md).  
  
9. En **valor**, seleccione el nombre de la imagen de la lista desplegable.  
  
10. En **TransparentColor**, seleccione un valor de color que desea quitar de la imagen. Esto creará un aspecto uniforme para el puntero en el medidor.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a los punteros de un medidor &#40;Generador de informes y SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Agregar un medidor a un informe &#40;el generador de informes SSRS&#41;](report-design/add-a-gauge-to-a-report-report-builder-and-ssrs.md)   
 [Aplicar formato a líneas, colores e imágenes &#40;Generador de informes y SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Medidores &#40;Generador de informes y SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  