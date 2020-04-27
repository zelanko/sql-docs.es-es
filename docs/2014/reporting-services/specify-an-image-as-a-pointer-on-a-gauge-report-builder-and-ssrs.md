---
title: Especificar una imagen como puntero en un medidor (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9d73b3c3-a068-4868-a2be-0cd261b6e92b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c7a57987a5d1cd0ac7984db3b716521d9c7a09af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101144"
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
  
2.  Opta Si no existe ningún puntero en el medidor, haga clic con el botón derecho en el medidor y seleccione **Agregar puntero**. Se agregará un puntero al medidor.  
  
3.  Haga clic en la pestaña **Insertar** de la cinta de opciones y haga doble clic en el icono de imagen. Se abrirá el cuadro de diálogo **Propiedades de la imagen**.  
  
4.  Agregue una imagen al informe. Para obtener más información, vea [incrustar una imagen en un informe &#40;generador de informes y SSRS&#41;](report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md).  
  
5.  Abra el panel de propiedades.  
  
6.  En la superficie de diseño, haga clic en el puntero. Las propiedades del puntero se muestran en el panel de propiedades.  
  
7.  Expanda el nodo PointerImage.  
  
8.  En **origen**, seleccione **incrustado** en la lista desplegable.  
  
    > [!NOTE]  
    >  Si la imagen está almacenada en la base de datos o en Internet, puede especificar la opción adecuada para esta propiedad. Para obtener más información, vea propiedades de la [imagen (cuadro de diálogo), General &#40;generador de informes y SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md).  
  
9. En **valor**, seleccione el nombre de la imagen en la lista desplegable.  
  
10. En **TransparentColor**, seleccione un valor de color que desee quitar de la imagen. Esto creará un aspecto uniforme para el puntero en el medidor.  
  
## <a name="see-also"></a>Consulte también  
 [Aplicar formato a los punteros de un medidor &#40;Generador de informes y SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Agregar un medidor a un informe &#40;Generador de informes y SSRS&#41;](report-design/add-a-gauge-to-a-report-report-builder-and-ssrs.md)   
 [Aplicar formato a líneas, colores e imágenes &#40;Generador de informes y SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Medidores &#40;Generador de informes y SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  
