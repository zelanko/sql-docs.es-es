---
title: "Comportamientos de la representaci&#243;n (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8f873ef9-27a3-40e5-b58b-6774f8027a58
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 7
---
# Comportamientos de la representaci&#243;n (Generador de informes y SSRS)
  Dependiendo del representador que seleccione, se aplican ciertas reglas al cuerpo del informe y a su contenido al representar un informe. La forma en la que los elementos de informe se ajustan en una página viene determinada por la combinación de estos factores:  
  
-   Reglas de representación.  
  
-   El ancho y alto de los elementos de informe.  
  
-   El tamaño del cuerpo del informe.  
  
-   El ancho y alto de la página.  
  
-   La compatibilidad específica del representador con la paginación.  
  
 En este tema se analizan las reglas generales aplicadas por Reporting Services. Para obtener más información, vea [Representar elementos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md), [Representar regiones de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-data-regions-report-builder-and-ssrs.md) y [Representar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-data-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Comportamientos generales para HTML, MHTML, Word y Excel (representadores de saltos de página automáticos)  
 Los informes exportados usando los formatos HTML y MHTML están optimizados para una visualización en pantalla, en la que las páginas pueden tener distintas longitudes. Los saltos de página solo se insertan verticalmente en ubicaciones aproximadas dentro del cuerpo del informe. El valor de alto interactivo del panel de propiedades determina estas ubicaciones aproximadas. Por ejemplo, imagine que el alto interactivo se establece en 5 pulgadas. Cuando se representa el informe, el alto de página tiene una longitud de aproximadamente 5 pulgadas. Word y Excel realizan la paginación basándose en los saltos de página lógicos y omiten el valor de alto interactivo.  
  
> [!NOTE]  
>  Para determinar cómo aparecerá un informe en un representador de saltos de página automáticos, use la vista previa del informe. El informe aparece como lo haría en un formato HTML, MHTML, Word o Excel.  
  
 Al exportar un informe a HTML, MHTML, Word o Excel, se siguen las reglas generales siguientes:  
  
-   Los saltos de página lógicos, los saltos de página que se insertan explícitamente, se aplican a los elementos de informe. Por ejemplo, si inserta un salto de página entre cada grupo, los saltos se aplican al representar el informe.  
  
-   Se crea un diseño aproximado usando el alto de página y el número de veces que aparece el elemento de informe. Por ejemplo, si un cuadro de texto tiene 0,5 pulgadas de alto y se repite cinco veces en el informe, se reservan 2,5 pulgadas.  
  
-   Se insertan varios saltos de página automáticos en función del valor de alto interactivo. Para suprimirlos en HTML y en los controles ReportViewer, y controlar la paginación únicamente con saltos de página explícitos, establezca el valor **interactive height** en 0 o en un número extremadamente grande.  
  
    > [!NOTE]  
    >  El valor de ancho interactivo no se utiliza en los representadores de saltos de página automáticos.  
  
-   Las páginas del informe pueden aumentar de tamaño para dar cabida a las líneas viudas y huérfanas, así como a los elementos de informe que se deben mantener juntos. Esto significa que el informe se puede extender más allá del ancho de la pantalla y se puede ver mediante las barras de desplazamiento.  
  
-   La paginación solo se aplica verticalmente a los informes.  
  
-   No se aplican los márgenes de página.  
  
## Comportamientos generales para PDF, Imagen e Imprimir (representadores de saltos de página duros)  
 Los informes exportados usando los formatos PDF e Imagen están optimizados para el formato impreso, en el que las páginas tienen un tamaño uniforme. Los saltos de página se insertan vertical y horizontalmente en ubicaciones concretas dentro del cuerpo del informe. La configuración del ancho y alto de página determina estas ubicaciones concretas.  
  
> [!NOTE]  
>  Para determinar cómo aparecerá un informe en un representador de saltos de página duros, use la vista previa de impresión. El informe aparecerá como lo haría en un formato PDF o Imagen.  
  
-   Las páginas se numeran secuencialmente de izquierda a derecha y de arriba abajo.  
  
-   Los saltos de página lógicos, los saltos de página que se insertan explícitamente, se aplican a los elementos de informe. Estos saltos de página pueden ocasionar que los elementos de informe desplacen otros elementos a la página siguiente.  
  
-   Si se produce un salto de página físico en elementos de informe que se deben mantener unidos, estos elementos se mueven a la página siguiente.  
  
-   Debido a las restricciones de tamaño de la página, es posible que no se puedan mantener unidos todos los elementos o repetir los elementos. Si sucede esto, el representador podría omitir ciertas reglas para la repetición con otro elemento para que el elemento de informe quepa en la página.  
  
-   Si no se puede mantener unido un elemento, por ejemplo un cuadro de texto que se hace demasiado grande como para caber dentro del área de página utilizable vertical, dicho elemento se recortará en el límite de página físico y continuará en la página siguiente.  
  
-   La paginación se aplica vertical y horizontalmente a los informes.  
  
    > [!NOTE]  
    >  El valor de ancho interactivo no se utiliza en los representadores de saltos de página duros.  
  
## Espaciado mínimo entre los elementos de informe  
 El tamaño de los elementos de informe aumenta dentro del cuerpo del informe para dar cabida a su contenido. Por ejemplo, una región de datos de matriz normalmente se expande por la página al representar el informe, y el alto de un cuadro de texto se ajusta dependiendo de los datos devueltos por una expresión.  
  
 Los representadores mantienen el espacio mínimo entre los elementos de informe definidos en el diseño del informe. Cuando se coloca un elemento de informe junto a otro en el diseño del informe, la distancia entre los elementos de informe se convierte en la distancia mínima que se debe mantener a medida que el informe crece horizontal o verticalmente. Por ejemplo, si agrega una región de datos de matriz a un informe y, a continuación, agrega un rectángulo situado 0,25 pulgadas a la derecha de la matriz, este espacio se mantiene a medida que la matriz aumenta de tamaño. Cada elemento se desplaza hacia la derecha para mantener la distancia mínima entre él y los que acaban a su izquierda.  
  
## Encabezados y pies de página  
 Los encabezados y pies de página aparecen en la parte superior e inferior de cada página representada. Puede dar formato al encabezado y al pie de página, y asignar un color, un estilo y un ancho a los bordes. También puede agregar un color o una imagen de fondo. Todas estas opciones de formato se representan dependiendo del formato elegido.  
  
 Las reglas siguientes se aplican a los encabezados y pies de página cuando se representan en el formato de representación HTML o MHTML:  
  
> [!NOTE]  
>  Para obtener información sobre cómo representa Excel los encabezados y pies de página, vea [Exportar a Microsoft Excel &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md). Para obtener información sobre cómo representa Word los encabezados y pies de página, vea [Exportar a Microsoft Word &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md).  
  
-   Cuando se definen, el encabezado y el pie de página se representan en la parte superior e inferior de cada página dentro del área de página utilizable.  
  
-   En las páginas donde el encabezado o el pie de página está oculto, el alto de éste se sigue reservando dentro del área de página utilizable, aunque el encabezado o el pie de página no se represente.  
  
-   Si el contenido del encabezado o del pie de página aumenta más allá de los límites de éste, el encabezado o el pie de página aumentará de tamaño para dar cabida al contenido.  
  
 Las reglas siguientes se aplican a los encabezados y pies de página cuando se representan en el formato de representación PDF o Imagen:  
  
-   El encabezado o el pie de página se representa en la parte superior e inferior de cada página dentro del área de página utilizable.  
  
-   En las páginas donde el encabezado o el pie de página está oculto, el alto de éste se sigue reservando dentro del área de página utilizable, aunque el encabezado o el pie de página no se represente.  
  
-   El encabezado y el pie de página no aumentan ni disminuyen de tamaño. Se representan en cada página con el alto que se especificó al crearlos.  
  
-   Independientemente del número de columnas que existan dentro del informe, solo hay un encabezado y un pie de página por página.  
  
-   Si el contenido del encabezado o del pie de página aumenta más allá de los límites de éste, se recorta el contenido.  
  
-   Los encabezados y pies de página que se definen en el archivo RDL original no se representan cuando el informe se representa como un subinforme.  
  
## Saltos de página lógicos  
 Los saltos de página lógicos son saltos de página que se insertan manualmente antes o después de los elementos de informe o los grupos. Los saltos de página ayudan a determinar cómo se ajusta el contenido a una página del informe para una visualización óptima a la hora de representar o exportar el informe.  
  
 Las reglas siguientes se aplican al representar los saltos de página lógicos:  
  
-   Los saltos de página lógicos se omiten para los elementos de informe que están siempre ocultos y para aquellos cuya visibilidad se controla haciendo clic en otro elemento de informe.  
  
-   Los saltos de página lógicos se aplican a los elementos visibles condicionalmente si éstos están visibles en el momento en el que se representa el informe.  
  
-   Se conserva el espacio entre el elemento de informe con el salto de página lógico y sus elementos de informe del mismo nivel.  
  
-   Los saltos de página lógicos que se insertan antes de un elemento de informe desplazan este a la página siguiente. El elemento de informe se representa en la parte superior de la página siguiente.  
  
-   No se mantienen los saltos de página lógicos definidos en elementos en celdas de tablas o matriz. Esto no se aplica a los elementos en listas.  
  
## Vea también  
 [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/interactive functionality - different report rendering extensions.md)   
 [Representar en HTML &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/rendering-to-html-report-builder-and-ssrs.md)   
 [Representación y diseño de páginas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/page-layout-and-rendering-report-builder-and-ssrs.md)  
  
  