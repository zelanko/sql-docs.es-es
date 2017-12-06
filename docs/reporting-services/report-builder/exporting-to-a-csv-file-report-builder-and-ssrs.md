---
title: Exportar a un archivo CSV (Generador de informes y SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-builder
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 68ec746e-8c82-47f5-8c3d-dbe403a441e5
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a41d99b7087463d5583e9cbb194175118dcab583
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="exporting-to-a-csv-file-report-builder-and-ssrs"></a>Exportar a un archivo CSV (Generador de informes y SSRS)
  La extensión de representación de valores separados por comas (CSV) representa los informes paginados como una representación sin estructura jerárquica de los datos a partir de un informe estándar de texto sin formato para que resulten fáciles de leer e intercambiar con muchas aplicaciones.  
  
 La extensión de representación CSV usa un delimitador de caracteres de cadena para separar los campos y las filas, y permite configurar dicho delimitador para que sea otro carácter distinto de la coma. El archivo resultante puede abrirse en un programa de hoja de cálculo como [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] o usarse como un formato de importación para otros programas. El informe exportado se convierte en un archivo .csv y devuelve un tipo MIME de **text/csv**.  
  
 Si desea trabajar con datos relacionados con gráficos, barras de datos, minigráficos, medidores e indicadores en [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)], exporte el informe a un archivo CSV y, a continuación, abra el archivo en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  
  
 Vea [Exportar informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) Para más información sobre cómo exportar a formato CSV.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CSVRendering"></a> Representación en CSV  
 Los informes CSV representados con la configuración predeterminada presentan las siguientes características:  
  
-   La cadena delimitadora de campos predeterminada es una coma (,).  
  
    > [!NOTE]  
    >  Puede cambiar el delimitador de campo por cualquier carácter que desee, incluido TAB; para ello, solo tiene que cambiar la configuración de la información del dispositivo. Para obtener más información, consulte [CSV Device Information Settings](../../reporting-services/csv-device-information-settings.md).  
  
-   La cadena delimitadora de registros es el retorno de carro y el avance de línea (\<cr>\<lf>).  
  
-   La cadena calificadora de texto es el signo de comillas tipográficas (").  
  
     El representador de CSV no agrega calificadores alrededor de todas las cadenas de texto. Los calificadores de texto solo se agregan cuando el valor contiene el carácter delimitador o cuando tiene un salto de línea.  
  
-   Si el texto contiene una cadena delimitadora incrustada o una cadena calificadora, el texto se incluye entre calificadores de texto y se duplican las cadenas calificadoras incrustadas.  
  
-   Se omite tanto el formato como el diseño.  
  
 Durante la representación no se tienen en cuenta los elementos siguientes:  
  
-   Encabezado de página  
  
-   Pie de página  
  
-   Elementos de informes personalizados  
  
-   Línea  
  
-   Imagen  
  
-   Rectángulo  
  
-   Subtotales automáticos  
  
 El resto de los elementos del informe se ordenan de arriba a abajo y, a continuación, de izquierda a derecha. Cada elemento se representa en una columna. Si el informe contiene elementos de datos anidados, como listas o tablas, los elementos primarios se repiten en cada registro.  
  
 En la tabla siguiente se indica el aspecto de los elementos de informe cuando se representan:  
  
|Elemento|Comportamiento de la representación|  
|----------|------------------------|  
|Cuadro de texto|Representa el contenido del cuadro de texto. En el modo predeterminado, se da formato a los elementos según las propiedades de formato de los mismos. En modo compatible, la configuración de la información del dispositivo puede cambiar el formato. Para obtener más información sobre los modos de representación de CSV, vea la sección correspondiente a continuación.|  
|Tabla|Realiza la representación mediante la expansión de la tabla y la creación de una fila y una columna para cada fila y columna del nivel máximo de detalle. Las filas y columnas de subtotal no tienen encabezados de columna ni de fila. No se admiten informes detallados.|  
|Matriz|Realiza la representación mediante la expansión de la matriz y la creación de una fila y una columna para cada fila y columna del nivel máximo de detalle. Las filas y columnas de subtotal no tienen encabezados de columna ni de fila.|  
|Lista|Representa un registro para cada instancia o fila de detalle de la lista.|  
|Subinforme|El elemento primario se repite en todas las instancias del contenido.|  
|Gráfico|Se representa mediante la creación de una fila para cada valor de gráfico y etiquetas de miembro. Las etiquetas de las series y las categorías de las jerarquías se quitan y se incluyen en la fila de un valor de gráfico.|  
|Barra de datos|Se representa como un gráfico. Normalmente, una barra de datos no incluye jerarquías ni etiquetas.|  
|Minigráfico|Se representa como un gráfico. Normalmente, un minigráfico no incluye jerarquías ni etiquetas.|  
|Medidor|Se representa como un único registro con los valores máximo y mínimo de la escala lineal, los valores inicial y final del intervalo, y el valor del puntero.|  
|Indicador|Se representa como un único registro con el nombre del estado activo, los estados disponibles y el valor de los datos.|  
|Mapa|Se representa como una fila con las etiquetas y los valores para cada miembro de mapa de una capa de mapa.<br /><br /> Si el mapa tiene varias capas, los valores de las filas varía, en función de si las capas de mapa usan las mismas regiones de datos de mapa u otras diferentes. Si varias capas de mapa utilizan la misma región de datos, las filas contienen datos de todas.|  
  
### <a name="hierarchical-and-grouped-data"></a>Datos jerárquicos y agrupados  
 Para que los datos jerárquicos y los datos agrupados puedan representarse en el formato CSV, es necesario quitar la información de estructura jerárquica.  
  
 La extensión de representación quita información de estructura jerárquica en el informe y lo convierte en una estructura de árbol que representa los grupos anidados dentro de la región de datos. Para quitar información de estructura jerárquica en el informe:  
  
-   Se quita información de estructura jerárquica de las jerarquías de fila antes que de las jerarquías de columna.  
  
-   Las columnas se ordenan de la manera siguiente: los cuadros de texto del cuerpo se ordenan de izquierda a derecha y de arriba abajo seguidos por las regiones de datos, que se ordenan de izquierda a derecha y de arriba abajo.  
  
-   Dentro de una región de datos, las columnas se ordenan de la manera siguiente: los miembros de las esquinas, los miembros de la jerarquía de fila, los miembros de la jerarquía de columna y, a continuación, las celdas.  
  
-   Las regiones de datos del mismo nivel son regiones de datos o grupos dinámicos que comparten una región de datos común o un antecesor dinámico. Los datos del mismo nivel se identifican creando una bifurcación del árbol sin información de estructura jerárquica.  
  
 Para obtener más información, consulte [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
  
##  <a name="RenderingModes"></a> Modos de representador  
 La extensión de representación CSV puede funcionar en dos modos: uno está optimizado para Excel; el otro está optimizado para aplicaciones de terceros que requieren un cumplimiento estricto de CSV con la especificación para CSV de RFC 4180. Dependiendo del modo que use, las regiones de datos del mismo nivel se administran de manera diferente.  
  
### <a name="default-mode"></a>Modo predeterminado  
 El modo predeterminado está optimizado para Excel. En modo predeterminado, el informe se representa como un archivo CSV con varias secciones de datos representados en CSV. Una línea vacía delimita cada región de datos del mismo nivel. Las regiones de datos del mismo nivel incluidas en el cuerpo del informe se representan como bloques de datos independientes dentro del archivo CSV. El resultado es un archivo CSV en el que:  
  
-   Los cuadros de texto individuales incluidos en el cuerpo del informe se representan una vez como el primer bloque de datos dentro del archivo CSV.  
  
-   Cada región de datos del mismo nivel de nivel superior existente en el cuerpo del informe se representa en su propio bloque de datos.  
  
-   Las regiones de datos anidadas se representan diagonalmente en el mismo bloque de datos.  
  
#### <a name="formatting"></a>Formato  
 Los valores numéricos se representan en su estado con formato. Excel puede reconocer valores numéricos con formato, como moneda, porcentaje y fecha, y puede dar formato a las celdas de forma adecuada al importar el archivo CSV.  
  
### <a name="compliant-mode"></a>Modo compatible  
 El modo compatible está optimizado para aplicaciones de terceros.  
  
#### <a name="data-regions"></a>Regiones de datos  
 Solo la primera fila del archivo contiene los encabezados de columna y cada fila tiene el mismo número de columnas.  
  
#### <a name="formatting"></a>Formato  
 Se quita el formato a los valores.  
  
##  <a name="Interactivity"></a> Interactividad  
 Ningún formato CSV generado por este representador admite la interactividad. No se representan los elementos interactivos siguientes:  
  
-   Hipervínculos  
  
-   Mostrar u ocultar  
  
-   Mapa del documento  
  
-   Vínculos de obtención de detalles o vínculos click-through  
  
-   Ordenación de usuarios finales  
  
-   Encabezados fijos  
  
-   Marcadores  
  
  
##  <a name="DeviceInfo"></a> Configuración de la información del dispositivo  
 Mediante la modificación de la configuración de la información del dispositivo, puede cambiar algunos valores de configuración predeterminados para este representador, incluidos el modo de representación, los caracteres que se usarán como delimitadores y los caracteres que se usarán como cadena predeterminada para el calificador de texto. Para obtener más información, consulte [CSV Device Information Settings](../../reporting-services/csv-device-information-settings.md).  
  
  
## <a name="see-also"></a>Vea también  
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Representar elementos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
