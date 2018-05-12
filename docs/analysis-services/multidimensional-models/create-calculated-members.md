---
title: Crear miembros calculados | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a0cee9d01fb55ace4d7062f96b5d3ea16c026669
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-calculated-members"></a>Crear miembros calculados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Puede crear medidas o miembros de una dimensión personalizados, denominados miembros calculados, combinando datos del cubo, operadores aritméticos, números y funciones. Por ejemplo, puede crear un miembro calculado denominado Euros que convierta dólares en euros multiplicando una medida de dólar existente por una tasa de cambio. De esta manera, se puede mostrar a los usuarios finales el valor en euros en una fila o una columna independiente.  
  
 Las definiciones de los miembros calculados se almacenan, pero sus valores solo existen en la memoria. En el ejemplo anterior, los usuarios finales ven los valores en euros, pero éstos no se almacenan como datos del cubo.  
  
 Los miembros calculados se crean en cubos. Para crear un miembro calculado, en el Diseñador de cubos, en la pestaña **Cálculos** , haga clic en el icono de **Nuevo miembro calculado** de la barra de herramientas. Este comando abre un formulario para especificar las siguientes opciones para el miembro calculado:  
  
 **Nombre**  
 Seleccione el nombre del miembro calculado. Este nombre aparece como encabezado de columna o de fila de los valores de miembros calculados cuando los usuarios finales examinan el cubo.  
  
 **Jerarquía primaria**  
 Seleccione la jerarquía primaria que se incluirá en el miembro calculado. Las jerarquías son categorías descriptivas de una dimensión mediante las cuales se pueden separar los datos numéricos (es decir, las medidas) de un cubo para su análisis. En los exploradores tabulares, las jerarquías proporcionan los encabezados de columna y de fila que se muestran a los usuarios finales cuando examinan los datos de un cubo. (En los exploradores gráficos, proporcionan otros tipos de etiquetas descriptivas pero tienen la misma función que en los exploradores tabulares). Un miembro calculado proporciona un nuevo encabezado (o etiqueta) en la dimensión primaria que seleccione.  
  
 Otra posibilidad es incluir el miembro calculado en las medidas, en vez de una dimensión. Esta opción también proporciona un nuevo encabezado de columna o de fila pero, en el explorador, se adjunta a las medidas.  
  
 **Miembro primario**  
 Haga clic en **Cambiar** para seleccionar un miembro primario para incluir el miembro calculado. Esta opción no está disponible si selecciona una jerarquía de un solo nivel o MEASURES como dimensión primaria.  
  
 Las jerarquías se dividen en niveles que contienen miembros. Cada miembro produce un encabezado. Mientras examinan los datos de un cubo, los usuarios finales pueden obtener detalles de un encabezado seleccionado a cualquier encabezado subordinado que no se haya mostrado previamente. El encabezado del miembro calculado se agrega al nivel inmediatamente inferior del miembro primario que haya seleccionado.  
  
 **Expresión**  
 Especifique la expresión que produce los valores del miembro calculado. Esta expresión puede escribirse en expresiones multidimensionales (MDX). La expresión puede contener cualquiera de los elementos siguientes:  
  
-   Expresiones de datos que representan los componentes del cubo, como dimensiones, niveles, medidas, etc.  
  
-   Operadores aritméticos  
  
-   Números  
  
-   Funciones  
  
 Puede arrastrar o copiar componentes del cubo desde la pestaña **Metadatos** del panel **Herramientas de cálculo** , para agregarlos rápidamente a una expresión.  
  
> [!IMPORTANT]  
>  Cualquier miembro calculado que vaya a utilizarse en la expresión de valor de otro miembro calculado debe crearse antes que el miembro calculado que va a utilizarlo.  
  
 Cadena de formato  
 Especifica el formato de los valores de celda que se basan en el miembro calculado. Esta propiedad acepta los mismos valores que la propiedad **Display Format** para las medidas. Para más información sobre los formatos de presentación, vea [Configurar propiedades de medidas](../../analysis-services/multidimensional-models/configure-measure-properties.md).  
  
 Visible  
 Determina si el miembro calculado queda visible u oculto cuando se recuperan los metadatos del cubo. Si el miembro calculado está oculto, se puede seguir usando en scripts, instrucciones y expresiones MDX, pero no aparece como objeto seleccionable en las interfaces de usuario cliente.  
  
 Comportamiento si no está vacío  
 Almacena los nombres de las medidas usadas para resolver las consultas NON EMPTY en MDX. Si la propiedad está en blanco, es necesario evaluar repetidamente el miembro calculado para determinar si está vacío. Si la propiedad contiene el nombre de una o más medidas, el miembro calculado se trata como si estuviera vacío cuando todas las medidas especificadas están vacías. Esta propiedad es una sugerencia de optimización para que Analysis Services solamente devuelva registros no NULL. Si solo se devuelven registros no NULL, mejora el rendimiento de las consultas MDX que utilizan el operador NON EMPTY o la función NonEmpty, o que exigen el cálculo de los valores de las celdas. Para mejorar el rendimiento de los cálculos de las celdas, especifique un solo miembro siempre que sea posible.  
  
 Expresiones de color  
 Especifica expresiones MDX que establecen dinámicamente los colores de primer plano y de fondo de las celdas en función del valor del miembro calculado. Esta propiedad se omite si las aplicaciones cliente no la admiten.  
  
 Expresiones de fuente  
 Especifica expresiones MDX que establecen dinámicamente la fuente, el tamaño de la fuente y los atributos de la fuente de las celdas en función del valor del miembro calculado. Esta propiedad se omite si las aplicaciones cliente no la admiten.  
  
 Puede arrastrar o copiar los componentes del cubo desde la pestaña **Metadatos** del panel **Herramientas de cálculo** al cuadro **Expresión** del panel de las expresiones de cálculo. Puede arrastrar o copiar funciones desde la pestaña **Funciones** del panel **Herramientas de cálculo** al cuadro **Expresión** del panel de las expresiones de cálculo.  
  
## <a name="addressing-calculated-members"></a>Direcciones en miembros calculados  
 Al crear un miembro calculado en la pestaña **Cálculos** del **Diseñador de cubos**, se especifica la jerarquía primaria en la que se almacena el miembro calculado. La jerarquía primaria determina cómo se pueden asignar direcciones a un miembro calculado, según las siguientes reglas:  
  
-   Si un miembro calculado se crea en la dimensión de medidas, el miembro calculado puede tener direcciones en esa dimensión.  
  
## <a name="see-also"></a>Vea también  
 [Cálculos en modelos multidimensionales](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
