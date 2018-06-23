---
title: Detectar categorías (herramientas de análisis de tabla para Excel) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Table Analysis tools
- clustering [data mining]
- mining model, decision tree
- category detection
ms.assetid: 3c7e9ebb-d0c9-498e-a9ba-cc13eaa43520
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d46840e2c2f7de1d56d6b528706ae908e7627a3e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108457"
---
# <a name="detect-categories-table-analysis-tools-for-excel"></a>Detectar categorías (Herramientas de análisis de tabla para Excel)
  ![Botón de categorías de detectar en la cinta de opciones](media/tat-detectcat.gif "botón detectar categorías en cinta de opciones")  
  
 El **detectar categorías** herramienta busca automáticamente las filas de una tabla que tienen características similares.  
  
 Cuando la herramienta finaliza, genera un informe que muestra las categorías encontradas junto con sus características distintivas. De forma predeterminada, agrega una nueva columna a la tabla de datos que contiene la categoría propuesta para cada fila de datos. Después, podrá revisar las categorías y cambiar su nombre.  
  
## <a name="using-the-detect-categories-tool"></a>Usar la herramienta Detectar categorías  
  
1.  Abra una tabla de Excel.  
  
2.  Haga clic en **detectar categorías**.  
  
3.  Especifique las columnas que desea usar en el análisis. Puede anular la selección de las columnas que tengan valores distintivos, como nombres de persona o identificadores de registro, ya que estas columnas podrían no ser útiles para el análisis.  
  
4.  Opcionalmente, especifique el número máximo de categorías que desea crear. De forma predeterminada, la herramienta crea automáticamente tantas categorías como encuentra.  
  
5.  Haga clic en **Ejecutar**.  
  
6.  La herramienta crea una nueva hoja de cálculo, denominada Informe de categorías, que contiene la lista de categorías y sus características.  
  
 Para obtener más información sobre cómo especificar opciones de la herramienta, consulte [detectar el cuadro de diálogo de categorías (herramientas de análisis de tabla para Excel)](detect-categories-table-analysis-tools-for-excel.md).  
  
## <a name="understanding-the-categories-report"></a>Descripción del Informe de categorías  
 El **informe de categorías** contiene dos tablas, **lista de categorías** y **características de categoría**y un **perfiles de categoría** gráfico.  
  
### <a name="category-list"></a>Lista de categorías  
 La primera tabla enumera las categorías que se encontraron. El **recuento de filas** columna indica el número de filas de datos se ha asignado a cada categoría.  
  
 El modelo crea nombres temporales para cada categoría, pero puede cambiar el nombre de las categorías como desee. Por ejemplo, en el ejemplo siguiente, se cambió la primera categoría **Low Income**, porque ese era el atributo superior del clúster.  
  
 ![informe creado por la herramienta detectar categorías](media/dm13-tat-detectcat-report1.gif "informe creado por la herramienta detectar categorías")  
  
 En cuanto escribe la nueva etiqueta, el cambio se propaga al resto de gráficos así como a la lista de categorías agregada en la hoja de cálculo de los datos de origen.  
  
### <a name="category-characteristics"></a>Características de categoría  
 La segunda tabla, **características de categoría**, muestra detalles sobre la composición de cada categoría. Haga clic en el **filtro** situado en la parte superior de la **categoría** columna para centrarse en unas cuantas categorías.  
  
 ![informe creado por la herramienta detectar categorías](media/dm13-tat-detectcat-report2.gif "informe creado por la herramienta detectar categorías")  
  
 El sombreado en la columna, **importancia relativa**, indica la importancia que la combinación de atributo y valor sea como factor diferenciador. Cuanto más larga sea la barra, más posibilidades existen de que el atributo sea muy representativo de esta categoría.  
  
### <a name="categories-profile-chart"></a>Gráfico de perfil de categorías  
 El gráfico final de la **informe de categorías** hoja de cálculo, **perfiles de categoría**, es un interactivo **gráfico dinámico** que puede utilizar para reorganizar y ocultar campos, filtrar por valores y personalizar la apariencia del gráfico.  
  
 Excel 2013 proporciona ahora **estilos de gráfico** y **elementos de gráfico** controla directamente en la superficie de diseño que facilitan la tarea mejorar el diseño de gráfico.  
  
 ![informe creado por la herramienta detectar categorías](media/dm13-tat-detectcat-report3.gif "informe creado por la herramienta detectar categorías")  
  
## <a name="requirements"></a>Requisitos  
 El **detectar categorías** herramienta no tiene ningún requisito para la cantidad o el tipo de datos.  
  
> [!NOTE]  
>  Cuando se usa el **detectar categorías** herramienta, se crea una nueva columna, categoría, en la tabla de datos original. Si deja esta columna en la tabla de datos y después realiza operaciones de minería de datos posteriores, la presencia de esta columna podría influir en los resultados. Para asegurarse de que otras operaciones no se verán afectadas, debería hacer una copia de la tabla de datos sin la columna Categoría antes de usar otras herramientas de minería de datos.  
  
## <a name="related-tools"></a>Herramientas relacionadas  
 Cuando el **detectar categorías** herramienta analiza los datos, crea una estructura de minería de datos y el modelo de minería de datos mediante el [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de clústeres.  
  
 Después de haber creado un modelo de minería de datos mediante el uso de la **analizar Influenciadores clave** herramienta, puede utilizar el cliente de minería de datos para Excel para examinar el modelo y explorar las relaciones con más detalle. El Cliente de minería de datos para Excel es un complemento independiente que proporciona funciones de minería de datos más avanzadas. Para obtener información, consulte [examinar modelos en Excel &#40;complementos de minería de datos de SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md).  
  
 Para obtener más información acerca del uso de los datos de modelado capacidades en el cliente de minería de datos para Excel, vea [crear un modelo de minería de datos](creating-a-data-mining-model.md).  
  
 Para obtener más información acerca del algoritmo usado por el **detectar categorías** herramienta, vea el tema "Algoritmo de clústeres de Microsoft" en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de análisis de tabla para Excel](table-analysis-tools-for-excel.md)  
  
  