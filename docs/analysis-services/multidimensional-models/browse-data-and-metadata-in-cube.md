---
title: Examinar los datos y metadatos de un cubo | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5faf2a9d-df39-465f-9c81-a00d5cd63f5a
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 995c0c6426f3014e58d49d61aad9a379ad5bc65e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="browse-data-and-metadata-in-cube"></a>Examinar los datos y metadatos de un cubo
  Use la pestaña **Explorador** del Diseñador de cubos para examinar los datos de un cubo. Puede usar esta vista para examinar la estructura de un cubo y comprobar los datos, el cálculo, el formato y la seguridad de los objetos de la base de datos. Puede examinar rápidamente un cubo tal como lo ven los usuarios finales con las herramientas de elaboración de informes o con otras aplicaciones cliente. Si examina los datos de un cubo, podrá ver las distintas dimensiones, explorar en profundidad los miembros y segmentar las dimensiones.  
  
 Para poder examinar un cubo, debe procesarlo y conectarse de nuevo a él. Una vez procesado, abra la pestaña **Explorador** del Diseñador de cubos. Haga clic en el botón Volver a conectar de la barra de herramientas para actualizar la conexión.  
  
 La pestaña **Explorador** tiene tres recuadros: el recuadro Metadatos, el recuadro Filtro y el recuadro Datos. Use el panel Metadatos para examinar la estructura del cubo en formato de árbol. Use el recuadro Filtro situado en la parte superior de la pestaña **Explorador** para definir cualquier subcubo que desee examinar. Use el recuadro Datos para ver el conjunto de resultados y explorar en profundidad las jerarquías de dimensión.  
  
## <a name="setting-up-the-browser"></a>Configurar el Explorador  
 Para prepararse para examinar un cubo, puede especificar la perspectiva o la traducción que desea usar. Las medidas y las dimensiones se agregan al panel Datos y los filtros se especifican en el panel Filtro.  
  
##### <a name="specifying-a-perspective"></a>Especificar una perspectiva  
 Use la lista **Perspectiva** para elegir una de las perspectivas definidas para el cubo. Las perspectivas se definen en la pestaña **Perspectivas** del Diseñador de cubos. Para cambiar a una perspectiva distinta, seleccione la nueva perspectiva en la lista.  
  
##### <a name="specifying-a-translation"></a>Especificar una traducción  
 Use la lista **Idioma** para elegir la traducción que desea definir para el cubo. Las traducciones se definen en la pestaña **Traducciones** del Diseñador de cubos. La pestaña **Explorador** inicialmente muestra títulos para el idioma predeterminado, que se especifica mediante la propiedad **Language** del cubo. Para cambiar a otro idioma, seleccione el nuevo idioma en la lista.  
  
##### <a name="formatting-the-data-pane"></a>Dar formato al panel Datos  
 Puede dar formato a los títulos y a las celdas del panel Datos. Haga clic con el botón derecho en las celdas o los títulos a los que quiere dar formato y, después, haga clic en **Comandos y opciones**. Dependiendo de la selección, el cuadro de diálogo **Comandos y opciones** mostrará la configuración de **Formato**, **Filtrar y agrupar**, **Informe**y **Comportamiento**.  
  
## <a name="setting-up-the-data"></a>Configurar los datos  
  
##### <a name="adding-or-removing-measures"></a>Agregar o quitar medidas  
 Arrastre las medidas que desea examinar desde el recuadro Metadatos hasta el área de detalles del recuadro Datos, que es el gran recuadro vacío situado en la parte inferior derecha del área de trabajo. A medida que arrastra medidas adicionales, estas se agregan como columnas. Una línea vertical indica dónde se colocará cada medida adicional. Si arrastra la carpeta **Medidas** , todas las medidas se colocan en el área de detalles.  
  
 Para quitar una medida del área de detalles, arrástrela fuera del panel Datos o haga clic con el botón derecho en ella y, después, haga clic en **Eliminar** en el menú contextual.  
  
##### <a name="adding-or-removing-dimensions"></a>Agregar o quitar dimensiones  
 Arrastre las jerarquías o las dimensiones hasta las áreas de fila o filtro.  
  
 Si desea trabajar con varias dimensiones, utilice Analizar en Excel. Analizar en Excel es un método abreviado que inicia Excel si está instalado en el mismo equipo que [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Excel abrirá un libro que contiene una conexión existente a la base de datos actual y cargará una lista de campos de tabla dinámica con medidas y dimensiones. Para obtener más información, vea [Analizar en Excel &#40;pestaña Explorador, Diseñador de cubos&#41; &#40;Analysis Services - Datos multidimensionales&#41;](http://msdn.microsoft.com/library/890ed457-137e-44ac-9b2c-83344a1b8fc9).  
  
 Para quitar una dimensión, arrástrela fuera del panel Datos o haga clic con el botón derecho en ella y, después, haga clic en **Eliminar** en el menú contextual.  
  
##### <a name="adding-or-removing-filters"></a>Agregar o quitar filtros  
 Para agregar un filtro, puede usar cualquiera de estos dos métodos:  
  
-   Expanda una dimensión en el panel Metadatos y arrastre una jerarquía al panel Filtro.  
  
     \- O bien  
  
-   En el **dimensión** columna de la **filtro** panel, haga clic en  **\<Seleccionar dimensión >** y seleccione una dimensión en la lista, a continuación, haga clic en  **\<Seleccionar jerarquía >** en el **jerarquía** columna y seleccione una jerarquía en la lista.  
  
 Después de especificar la jerarquía, especifique el operador y la expresión de filtro. En la tabla siguiente se describen los operadores y las expresiones de filtro.  
  
|Operador|Expresión de filtro|Description|  
|--------------|-----------------------|-----------------|  
|Igual|Uno o varios miembros|Los valores deben ser iguales que un miembro especificado.<br /><br /> (Proporciona una selección de varios miembros para jerarquías de atributo que no sean jerarquías de elementos primarios y secundarios ni una selección de un único miembro de otras jerarquías).|  
|No igual|Uno o varios miembros|Los valores no deben ser iguales que un miembro especificado.<br /><br /> (Proporciona una selección de varios miembros para jerarquías de atributo que no sean jerarquías de elementos primarios y secundarios ni una selección de un único miembro de otras jerarquías).|  
|Entrada|Uno o varios conjuntos con nombre|Los valores deben estar en un conjunto con nombre especificado.<br /><br /> (Se admite solo para las jerarquías de atributo).|  
|No en|Uno o varios conjuntos con nombre|Los valores no deben estar en un conjunto con nombre especificado.<br /><br /> (Se admite solo para las jerarquías de atributo).|  
|Intervalo (Inclusivo)|Uno o dos miembros delimitadores de un intervalo|Los valores deben estar entre los miembros delimitadores o ser iguales que ellos. Si los miembros delimitadores son iguales o solo se ha especificado un miembro, no se impone ningún intervalo y se permiten todos los valores.<br /><br /> (Se admite solo para las jerarquías de atributo. El intervalo debe estar en un nivel de una jerarquía. Actualmente, no se admiten los intervalos sin límites).|  
|Intervalo (Exclusivo)|Uno o dos miembros delimitadores de un intervalo|Los valores deben estar entre los miembros delimitadores. Si los miembros delimitadores son iguales o solo se ha especificado uno, los valores deben ser mayores o menores que el miembro delimitador.<br /><br /> (Se admite solo para las jerarquías de atributo. El intervalo debe estar en un nivel de una jerarquía. Actualmente, no se admiten los intervalos sin límites).|  
|MDX|Expresión MDX que devuelve un conjunto de miembros|Los valores deben estar en el conjunto de miembros calculados. Cuando se selecciona esta opción, aparece el cuadro de diálogo **Generador de miembros calculados** para crear expresiones MDX.|  
  
 Para las jerarquías definidas por el usuario, en las que se pueden especificar varios miembros en la expresión de filtro, todos los miembros especificados deben estar en el mismo nivel y compartir el mismo elemento primario. Esta restricción no se aplica a las jerarquías de elementos primarios y secundarios.  
  
## <a name="working-with-data"></a>Trabajar con datos  
  
##### <a name="drilling-down-into-a-member"></a>Explorar en profundidad un miembro  
 Para explorar en profundidad un miembro determinado, haga clic en el signo más (+) situado junto al miembro o haga doble clic en este.  
  
##### <a name="slicing-through-cube-dimensions"></a>Segmentar dimensiones de cubo  
 Para filtrar los datos del cubo, haga clic en el cuadro de lista desplegable situado en el encabezado de columna de nivel superior. Puede expandir la jerarquía y activar o desactivar un miembro de cualquier nivel para mostrar u ocultar tanto el miembro como todos sus descendientes. Desactive la casilla situada junto a **(Todos)** para borrar todos los miembros de la jerarquía.  
  
 Después de haber configurado el filtro en las dimensiones, puede activarlo o desactivarlo; para ello, haga clic con el botón derecho en cualquier lugar del panel Datos y, después, haga clic en **Autofiltro**.  
  
##### <a name="filtering-data"></a>Filtrado de datos  
 Puede usar el área de filtro para definir un subcubo para examinarlo. Para agregar un filtro, puede hacer clic en una dimensión en el panel Filtro o puede expandir una dimensión en el panel Metadatos y arrastrar una jerarquía al panel Filtro. A continuación, especifique un **Operador** y una **Expresión de filtro**.  
  
##### <a name="performing-actions"></a>Realizar acciones  
 Un triángulo marca cualquier encabezado o celda del panel Datos para el que exista una acción. Esto puede aplicarse a una dimensión, un nivel, un miembro o una celda de un cubo. Mueva el puntero sobre el objeto de encabezado para ver una lista de acciones disponibles. Haga clic en el triángulo de la celda para mostrar un menú e iniciar el proceso asociado.  
  
 Por razones de seguridad, la pestaña **Explorador** solo admite las siguientes acciones:  
  
-   Dirección URL  
  
-   Conjunto de filas  
  
-   Obtención de detalles  
  
 No se admiten las acciones Línea de comandos, Instrucción y Propietario. Las acciones Dirección URL son seguras en la medida en que lo es la página web a la que vinculan.  
  
##### <a name="viewing-member-properties-and-cube-cell-information"></a>Ver las propiedades de los miembros e información sobre las celdas del cubo  
 Para ver información sobre un objeto de dimensión o un valor de celda, mueva el puntero sobre la celda.  
  
##### <a name="showing-or-hiding-empty-cells"></a>Mostrar u ocultar las celdas vacías  
 Para ocultar las celdas vacías de la cuadrícula de datos, haga clic con el botón derecho en cualquier lugar del panel Datos y, después, haga clic en **Mostrar celdas vacías**.  
  
  
