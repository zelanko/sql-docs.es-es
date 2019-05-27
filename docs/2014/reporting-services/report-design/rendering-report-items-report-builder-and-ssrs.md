---
title: Representar elementos de informe (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 99ebb4dc-41cc-42ac-82dd-a2b0e31155a0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ecd7088b9fe76b955cc40dd495d508878b9d0d96
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105353"
---
# <a name="rendering-report-items-report-builder-and-ssrs"></a>Representar elementos de informe (Generador de informes y SSRS)
  El número, tamaño y ubicación de los elementos de informe afectan a la manera en que los representadores paginan el cuerpo del informe. A continuación se incluye una descripción de cómo se representan los distintos elementos de informe.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="overlapping-report-items"></a>Elementos de informe superpuestos  
 Los elementos de informe superpuestos no se admiten en HTML, MHTML, Word, Excel, la vista previa ni el Visor de informes. Si existe algún elemento superpuesto, se mueve. A los elementos de informe se les aplican las reglas siguientes:  
  
-   Si es mayor la superposición vertical de los elementos de informe, uno de los elementos superpuestos se desplaza a la derecha. El elemento situado más a la izquierda permanece en su lugar.  
  
-   Si es mayor la superposición horizontal de los elementos de informe, uno de los elementos se desplaza hacia abajo. El elemento situado más arriba permanece en su lugar.  
  
-   Si la superposición vertical y la horizontal son iguales, uno de los elementos superpuestos se desplaza a la derecha. El elemento situado más a la izquierda permanece en su lugar.  
  
-   Si se debe mover un elemento para corregir la superposición, los elementos de informe adyacentes se desplazan hacia abajo y/o a la derecha para conservar una cantidad mínima de espacio entre el elemento y los elementos de informe que finalizan sobre él y/o a su izquierda. Por ejemplo, imagine que dos elementos de informe se superponen verticalmente y que un tercero está situado a 2 pulgadas a su derecha. Cuando el elemento de informe superpuesto se mueve hacia la derecha, el tercero se desplaza también hacia la derecha para conservar las 2 pulgadas existentes entre él y el elemento de informe de su izquierda.  
  
 Los elementos de informe superpuestos son compatibles con los formatos de saltos de página duros, incluyendo la impresión.  
  
## <a name="visibility-and-report-items"></a>Visibilidad y elementos de informe  
 Los elementos de informe se pueden ocultar o mostrar de forma predeterminada, o de forma condicional mediante expresiones. Opcionalmente, la visibilidad se puede cambiar haciendo clic en otro elemento de informe.  
  
 Se aplican las reglas de visibilidad siguientes al representar elementos de informe:  
  
-   Si un elemento de informe y su contenido están siempre ocultos (no se ocultan en función de una expresión o no se puede cambiar su visibilidad haciendo clic en otro elemento de informe), los elementos de informe situados a su derecha o por debajo no se mueven para rellenar el espacio vacío. Por ejemplo, si un rectángulo y la imagen que contiene están ocultos, el elemento de informe que comienza a la derecha del rectángulo no se mueve a la izquierda para rellenar lo que parece espacio vacío. Se conserva el espacio ocupado por el rectángulo.  
  
-   Si un elemento de informe y su contenido se ocultan condicionalmente (se ocultan en función de una expresión o su visibilidad se puede cambiar haciendo clic en otro elemento de informe), los elementos de informe situados a su derecha o por debajo se mueven a la izquierda para rellenar el espacio cuando se oculta el elemento.  
  
-   Si la visibilidad de un elemento de informe y su contenido se puede cambiar haciendo clic en otro elemento de informe, la paginación cambia para adaptarse al elemento de informe y su contenido solo cuando se muestra inicialmente.  
  
## <a name="keeping-report-items-together-on-a-single-page"></a>Mantener unidos los elementos de informe en una sola página  
 Muchos de los elementos de informe incluidos en un informe se pueden conservar unidos en una sola página de forma implícita o explícita estableciendo las propiedades KeepWithGroup o KeepTogether. Los elementos de informe siempre se representan en la misma página si el elemento de informe no tiene ningún salto de página lógico y es más pequeño que el área de página utilizable. Si un elemento de informe no cabe por completo en la página en la que normalmente se iniciaría, se inserta un salto de página duro antes de dicho elemento, forzando a que se muestre en la página siguiente. En los representadores de salto de página automático, la página aumenta de tamaño para dar cabida al elemento de informe.  
  
 Si el elemento de informe está oculto siempre, las reglas para mantener unidos los elementos se omiten.  
  
 Los siguientes elementos se mantienen siempre unidos:  
  
-   Imágenes.  
  
-   Líneas.  
  
-   Gráficos, medidores y mapas.  
  
-   Una fila única en una región de datos que aparece de forma separada en otra página, seleccionando la opción KeepWithGroup. Esto mantendrá unida de forma implícita la fila única con al menos una instancia del grupo para que la fila no quede huérfana. Puede establecer esta opción en una región de datos o un grupo.  
  
-   Área de encabezado de una región de datos.  
  
-   Área de encabezado de una región de datos y la primera fila de datos.  
  
-   Elementos de informe que se pueden activar o desactivar en una región de datos Tablix.  
  
### <a name="priority-order"></a>Orden de prioridad  
 Debido a las limitaciones de tamaño de la página, pueden surgir conflictos entre las reglas para mantener unidos los elementos de informe. En este caso, se usa el orden de prioridad siguiente para mantener unidos los elementos al efectuar la representación:  
  
-   Líneas, gráficos e imágenes.  
  
-   Control de líneas viudas y huérfanas.  
  
-   Encabezados de columna y encabezados de fila repetidos.  
  
     Los encabezados tienen prioridad sobre los pies de página. Los grupos repetidos internos tienen prioridad sobre los grupos externos. Los elementos en los que se establece la propiedad `RepeatWith` y que están más cerca de la región de datos de destino tienen prioridad sobre los elementos situados más lejos de dicha región.  
  
-   Elementos de informe pequeños, como cuadros de texto o rectángulos, con una propiedad KeepTogether explícita establecida en `true`.  
  
-   Elementos de informe de gran tamaño, como subinformes o un miembro de tablix que no sean más interno, con una propiedad KeepTogether explícita establecida en `true`.  
  
-   Regiones de datos Tablix con una propiedad KeepTogether explícita establecida en `true`.  
  
### <a name="subreports"></a>Subinformes  
 Un subinforme se representa como un rectángulo que contiene otro informe definido en un archivo de informe .rdl independiente. El archivo de subinforme se debe publicar en un servidor de informes para que el informe primario pueda tener acceso a él.  
  
 Se aplican las reglas siguientes al representar los subinformes:  
  
-   Los subinformes pueden crecer hasta tener el tamaño del cuerpo especificado en el archivo .rdl que define el subinforme. Por ejemplo, si el archivo RDL para el subinforme establece que el cuerpo del subinforme tiene 5 pulgadas de ancho, el subinforme tendrá 5 pulgadas de ancho dentro del informe primario.  
  
-   Los subinformes heredan la configuración de las columnas del informe primario. Las configuraciones de columnas definidas en el archivo RDL original siempre se omiten.  
  
-   Solo se representa el cuerpo del subinforme. Las secciones de encabezado y de pie de página definidas en el archivo .rdl del subinforme no se representan cuando el subinforme se representa en el informe primario.  
  
-   Los subinformes tienen una propiedad KeepTogether explícita. Cuando dicha propiedad se establece en `true`, todos los elementos del subinforme se mantendrán unidos en una página siempre que sea posible.  
  
-   Si un subinforme no se puede ejecutar, se muestra en el informe como un cuadro de texto con un mensaje de error. Las propiedades de estilo aplicadas al subinforme se aplican en su lugar al cuadro de texto.  
  
-   Si un salto de página divide el subinforme, el parámetro **Omitir borde en el salto de página** controla si los bordes del subinforme están cerrados o abiertos.  
  
 Para más información sobre los subinformes, vea [Subinformes &#40;Generador de informes y SSRS&#41;](subreports-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;Generador de informes y SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
