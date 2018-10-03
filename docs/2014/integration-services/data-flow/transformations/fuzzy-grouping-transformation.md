---
title: Transformación Agrupación aproximada | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtrans.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- Fuzzy Grouping transformation
- temporary tables [Integration Services]
- grouping data
- standardizing data [Integration Services]
- columns [Integration Services], standardizing
- similarity thresholds [Integration Services]
- data cleaning [Integration Services]
- duplicate data [Integration Services]
ms.assetid: e43f17bd-9d13-4a8f-9f29-cce44cac1025
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8f0b1fc213fb1916421b1c9b0f02bb82b5553770
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48123011"
---
# <a name="fuzzy-grouping-transformation"></a>Agrupación aproximada, transformación
  La transformación Agrupación aproximada realiza tareas de limpieza de datos, identificando filas de datos que probablemente se van a duplicar y seleccionando una fila de datos canónica para utilizarla en la normalización de los datos.  
  
> [!NOTE]  
>  Para más detalles sobre la transformación Agrupación aproximada, incluyendo las limitaciones de rendimiento y memoria, vea las notas del producto [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005 (Búsqueda y agrupación aproximada en SQL Server Integration Services 2005)](http://go.microsoft.com/fwlink/?LinkId=96604).  
  
 La transformación de Búsqueda aproximada requiere una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para crear las tablas temporales de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que necesita el algoritmo de la transformación para realizar su trabajo. La conexión debe establecerla un usuario que tenga permiso para crear tablas en la base de datos.  
  
 Para configurar la transformación, debe seleccionar las columnas de entrada que desee utilizar para identificar duplicados y el tipo de coincidencia, aproximada o exacta, para cada columna. Una coincidencia exacta garantiza que solo se agruparán las filas de la columna que tengan valores idénticos. La coincidencia exacta se puede aplicar a columnas con cualquier tipo de datos de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , excepto DT_TEXT, DT_NTEXT y DT_IMAGE. Una coincidencia aproximada agrupa filas que tienen aproximadamente el mismo valor. El método para la coincidencia aproximada de los datos se basa en la puntuación de similitud especificada por el usuario. Para la coincidencia aproximada, solo se pueden utilizar columnas con tipos de datos DT_WSTR y DT_STR. Para más información, consulte [Integration Services Data Types](../integration-services-data-types.md).  
  
 La salida de transformación incluye todas las columnas de entrada, una o más columnas con datos normalizados, y una columna que contiene la puntuación de similitud. La puntuación es un valor decimal entre 0 y 1. La fila canónica tiene una puntuación de 1. Las otras filas de la agrupación aproximada tienen puntuaciones que indican su nivel de coincidencia con la fila canónica. Cuanto más se acerque el resultado a 1, mayor será la coincidencia entre la fila y la fila canónica. Si la agrupación aproximada contiene filas que son duplicados exactos de la fila canónica, dichas filas también tienen una puntuación de 1. La transformación no quita las filas duplicadas. Se agrupan creando una clave que relaciona la fila canónica con las filas similares.  
  
 La transformación produce una fila de salida por cada fila de entrada, con las siguientes columnas adicionales:  
  
-   **_key_in**, una columna que identifica de forma única cada fila.  
  
-   **_key_out**, una columna que identifica un grupo de filas duplicadas. La columna **_key_out** tiene el valor de la columna **_key_in** en la fila de datos canónica. Las filas con el mismo valor en **_key_out** forman parte del mismo grupo. El valor **_key_out**de un grupo corresponde al valor de **_key_in** en la fila de datos canónicos.  
  
-   **_score**, un valor entre 0 y 1 que indica la similitud entre la fila de entrada y la fila canónica.  
  
 Éstos son los nombres de columna predeterminados y puede configurar la transformación Agrupación aproximada para que utilice otros. La salida también proporciona una puntuación de similitud para cada columna que participa en una agrupación aproximada.  
  
 La transformación Agrupación aproximada incluye dos características para personalizar la agrupación que realiza: delimitadores de token y umbral de similitud. La transformación proporciona un conjunto predeterminado de delimitadores que se utilizan para dividir los datos en tokens, pero puede agregar delimitadores nuevos que mejoren la división en tokens de los datos.  
  
 El umbral de similitud indica qué tan estricta es la transformación a la hora de identificar duplicados. Los umbrales de similitud se pueden establecer en el nivel de componente y de columna. El umbral de similitud en el nivel de columna solamente está disponible para las columnas que realizan una coincidencia aproximada. El intervalo de similitud es de 0 a 1. Cuanto más se acerque el umbral a 1, más similares deberán ser las filas y las columnas para ser calificadas como duplicados. El umbral de similitud entre filas y columnas se especifica estableciendo la propiedad MinSimilarity en los niveles de componente y de columna. Para satisfacer la similitud especificada en el nivel de componente, todas las filas deben tener una similitud en todas las columnas igual o superior al umbral de similitud especificado en el nivel de componente.  
  
 La transformación Agrupación aproximada calcula el valor interno de similitud y no agrupa las filas con un valor de similitud inferior al especificado en MinSimilarity.  
  
 Para identificar un umbral de similitud válido para sus datos, es posible que deba aplicar la transformación Agrupación aproximada varias veces utilizando distintos umbrales de similitud mínima. Durante la ejecución, las columnas de puntuación de la salida de transformación contienen las puntuaciones de similitud para cada fila de un grupo. Puede utilizar estos valores para identificar el umbral de similitud apropiado para sus datos. Si quiere aumentar la similitud, debe establecer MinSimilarity en un valor mayor que el valor de las columnas de puntuación.  
  
 Puede personalizar la agrupación que lleva a cabo la transformación, estableciendo las propiedades de las columnas en la entrada de la transformación Agrupación aproximada. Por ejemplo, la propiedad FuzzyComparisonFlags especifica cómo se compara la transformación los datos de cadena en una columna y la propiedad ExactFuzzy especifica si la transformación realiza una coincidencia aproximada o exacta.  
  
 La cantidad de memoria que usa la transformación Agrupación aproximada se puede configurar al establecer la propiedad personalizada MaxMemoryUsage. Puede especificar el número de megabytes (MB) o utilizar el valor 0 para permitir a la transformación utilizar una cantidad de memoria dinámica en función de sus necesidades y de la memoria física disponible. La propiedad personalizada MaxMemoryUsage se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada y una salida. No admite una salida de error.  
  
## <a name="row-comparison"></a>Comparar filas  
 Al configurar la transformación Agrupación aproximada, puede especificar el algoritmo de comparación que utiliza la transformación para comparar las filas de la entrada de la transformación. Si establece la propiedad Exhaustive en `true`, la transformación compara cada fila de la entrada con todas las demás filas en la entrada. Este algoritmo de comparación puede producir resultados más exactos, pero es probable que la transformación sea más lenta, a menos que el número de filas de la entrada sea pequeño. Para evitar problemas de rendimiento, es conveniente establecer la propiedad Exhaustive en `true` solo durante el desarrollo del paquete.  
  
## <a name="temporary-tables-and-indexes"></a>Tablas e índices temporales  
 Durante la ejecución, la transformación Agrupación aproximada crea objetos temporales, como tablas e índices, que pueden tener un tamaño considerable, en la base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a la que se conecta la transformación. El tamaño de las tablas y los índices es proporcional al número de filas de la entrada de la transformación y al número de tokens creados por la transformación Agrupación aproximada.  
  
 La transformación también consulta las tablas temporales. Por lo tanto, debe considerar la posibilidad de conectar la transformación Agrupación aproximada a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]que no sea de producción, en especial si el servidor de producción tiene un espacio en disco disponible limitado.  
  
 El rendimiento de esta transformación puede mejorar si las tablas e índices que utiliza están ubicados en el equipo local.  
  
## <a name="configuration-of-the-fuzzy-grouping-transformation"></a>Configuración de la transformación Agrupación aproximada  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Agrupación aproximada** , haga clic en uno de los temas siguientes:  
  
-   [Editor de transformación Agrupación aproximada &#40;pestaña Administrador de conexiones&#41;](../../fuzzy-grouping-transformation-editor-connection-manager-tab.md)  
  
-   [Editor de transformación Agrupación aproximada &#40;pestaña columnas&#41;](../../fuzzy-grouping-transformation-editor-columns-tab.md)  
  
-   [Editor de transformación Agrupación aproximada &#40;ficha Opciones avanzadas&#41;](../../fuzzy-grouping-transformation-editor-advanced-tab.md)  
  
 Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener información detallada sobre cómo establecer propiedades de esta tarea, haga clic en uno de los temas siguientes:  
  
-   [Identificación de filas de datos similares con la transformación Agrupación aproximada](fuzzy-grouping-transformation.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>Vea también  
 [Transformación Búsqueda aproximada](lookup-transformation.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
  
