---
title: Estimar el tamaño de un índice no agrupado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- clustered indexes, table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: c183b0e4-ef4c-4bfc-8575-5ac219c25b0a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: aa4b0d73d1cba3d612da9f666bb548dfbc54102f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054119"
---
# <a name="estimate-the-size-of-a-nonclustered-index"></a>Estimar el tamaño de un índice no clúster
  Siga estos pasos para estimar el espacio necesario para almacenar un índice no clúster:  
  
1.  Calcular las variables que deben usarse en los pasos 2 y 3.  
  
2.  Calcular el espacio utilizado para almacenar información del índice en el nivel hoja del índice no clúster.  
  
3.  Calcular el espacio utilizado para almacenar información del índice en los niveles no hoja del índice no clúster.  
  
4.  Sumar los valores calculados.  
  
## <a name="step-1-calculate-variables-for-use-in-steps-2-and-3"></a>Paso 1. Calcularlas variables que deben usarse en los pasos 2 y 3  
 Los siguientes pasos pueden utilizarse para calcular las variables que se utilizan para estimar el espacio necesario para almacenar los niveles superiores del índice:  
  
1.  Especifique el número de filas que habrá en la tabla:  
  
     ***Num_Rows***  = número de filas de la tabla  
  
2.  Especifique el número de columnas de longitud fija y variable de la clave de índice, y calcule el espacio necesario para su almacenamiento:  
  
     Las columnas de clave de un índice pueden incluir columnas de longitud fija y de longitud variable. Para estimar el tamaño de las filas de índice de nivel interior, calcule el espacio que ocupa cada uno de estos grupos de columnas en la fila de índice. El tamaño de una columna depende del tipo y de la longitud especificados para los datos.  
  
     ***Num_Key_Cols***  = número total de columnas de clave (de longitud fija y variable)  
  
     ***Fixed_Key_Size***  = tamaño total en bytes de todas las columnas de clave de longitud fija  
  
     ***Num_Variable_Key_Cols***  = número de columnas de clave de longitud variable  
  
     ***Max_Var_Key_Size***  = tamaño máximo en bytes de todas las columnas de clave de longitud variable  
  
3.  Tenga en cuenta el localizador de fila de datos necesario si el índice no es único:  
  
     Si el índice no clúster no es único, el localizador de fila de datos se combina con la clave de índice no clúster para generar un valor de clave único para cada fila.  
  
     Si el índice no clúster se encuentra sobre un montón, el localizador de fila de datos es el RID del montón. Tiene un tamaño de 8 bytes.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + 1  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + 1  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + 8  
  
     Si el índice no clúster se encuentra sobre un índice clúster, el localizador de fila de datos es la clave de agrupación en clústeres. Las columnas que se deben combinar con la clave de índice no clúster son las columnas de la clave de agrupación en clústeres que ya no están presentes en el conjunto de columnas de clave de índice no clúster.  
  
     ***Num_Key_Cols***  = ***Num_Key_Cols*** + número de columnas de clave de agrupación en clústeres no presentes en el conjunto de columnas de clave de índice no agrupado (+ 1 si el índice agrupado no es único)  
  
     ***Fixed_Key_Size***  = ***Fixed_Key_Size*** + tamaño total en bytes de las columnas de clave de agrupación en clústeres de longitud fija que no están presentes en el conjunto de columnas de clave de índice no agrupado  
  
     ***Num_Variable_Key_Cols***  = ***Num_Variable_Key_Cols*** + número de columnas de clave de agrupación en clústeres de longitud variable no presentes en el conjunto de columnas de clave de índice no agrupado (+ 1 si el índice agrupado no es único)  
  
     ***Max_Var_Key_Size***  = ***Max_Var_Key_Size*** + tamaño máximo en bytes de las columnas de clave de agrupación en clústeres de longitud variable no presentes en el conjunto de columnas de clave de índice no agrupado (+ 4 si el índice agrupado no es único)  
  
4.  Se puede reservar parte de la fila, conocida como el mapa de bits NULL, para administrar la nulabilidad de las columnas. Calcule el tamaño:  
  
     Si existen columnas que aceptan valores NULL en la clave del índice, incluidas las columnas de clave de agrupación en clústeres necesarias que se describen en el paso 1.3, se reserva parte de la fila de índice para el mapa de bits NULL.  
  
     ***Index_Null_Bitmap***  = 2 + ((número de columnas de la fila de índice + 7) / 8)  
  
     Solamente debe utilizarse la parte entera de la expresión anterior. Descarte el resto.  
  
     Si no existen columnas de clave que aceptan valores NULL, establezca ***Index_Null_Bitmap*** en 0.  
  
5.  Calcule el tamaño de los datos de longitud variable:  
  
     Si hay columnas de longitud variable en la clave de índice, incluidas las columnas de clave de índice clúster necesarias, determine cuánto espacio se utiliza para almacenar las columnas de la fila de índice:  
  
     ***Variable_Key_Size***  = 2 + (***Num_Variable_Key_Cols*** x 2) + ***Max_Var_Key_Size***  
  
     Los bytes agregados a ***Max_Var_Key_Size*** son para el seguimiento de cada columna de longitud variable. En esta fórmula se supone que todas las columnas de longitud variable están llenas al 100 %. Si prevé que va a usarse un porcentaje inferior del espacio de almacenamiento de columnas de longitud variable, puede ajustar el valor de ***Max_Var_Key_Size*** en función de ese porcentaje para obtener una estimación más precisa del tamaño global de la tabla.  
  
     Si no hay columnas de longitud variable, establezca ***Variable_Key_Size*** en 0.  
  
6.  Calcule el tamaño de la fila del índice:  
  
     ***Index_Row_Size***  = ***Fixed_Key_Size*** + ***Variable_Key_Size*** + ***Index_Null_Bitmap*** + 1 (para la sobrecarga de encabezado de una fila de índice) + 6 (para el puntero de identificador de página secundaria)  
  
7.  Calcule el número de filas de índice por página (8.096 bytes disponibles por página):  
  
     ***Index_Rows_Per_Page***  = 8096 / (***Index_Row_Size*** + 2)  
  
     Dado que las filas de índice no abarcan varias páginas, el número de filas de índice por página debe redondearse hacia abajo a la fila completa más cercana. El valor 2 de la fórmula representa la entrada de la fila en la matriz de zonas de la página.  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information-in-the-leaf-level"></a>Paso 2. Calcular el espacio utilizado para almacenar información del índice en el nivel hoja  
 Para estimar el espacio necesario para almacenar el nivel hoja del índice, puede utilizar los siguientes pasos. Para completar este paso, necesita los valores del Paso 1.  
  
1.  Especifique el número de columnas de longitud fija y variable en el nivel hoja y calcule el espacio necesario para su almacenamiento:  
  
    > [!NOTE]  
    >  Un índice no clúster se puede ampliar incluyendo columnas que no son de clave además de las columnas de clave de índice. Estas columnas adicionales solamente se almacenan en el nivel hoja del índice no clúster. Para más información, consulte [Create Indexes with Included Columns](../indexes/create-indexes-with-included-columns.md).  
  
    > [!NOTE]  
    >  Puede combinar las columnas `varchar`, `nvarchar`, `varbinary` o `sql_variant` que hagan que el ancho total definido para la tabla sea superior a 8.060 bytes. La longitud de cada una de estas columnas debe ajustarse al límite de 8.000 bytes en columnas `varchar`, `varbinary` o `sql_variant` y de 4.000 bytes en columnas `nvarchar`. Sin embargo, el ancho combinado puede superar el límite de 8.060 bytes de una tabla. Esto también se aplica a filas de hoja de índice no clúster con columnas incluidas.  
  
     Si el índice no clúster no incluye columnas, utilice los valores del Paso 1, incluidas las modificaciones determinadas en el Paso 1.3:  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols***  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size***  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols***  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size***  
  
     Si el índice no clúster no incluye columnas, agregue los valores apropiados a los valores del Paso 1, incluidas las modificaciones del Paso 1.3. El tamaño de una columna depende del tipo y de la longitud especificados para los datos. Para obtener más información, vea [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
     ***Num_Leaf_Cols***  = ***Num_Key_Cols*** + número de columnas incluidas  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Key_Size*** + tamaño total de bytes de las columnas de longitud fija incluidas  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Key_Cols*** + número de columnas de longitud variable incluidas  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Key_Size*** + tamaño máximo de bytes de todas las columnas de longitud variable incluidas  
  
2.  Tenga en cuenta el localizador de fila de datos:  
  
     Si el índice no clúster no es único, la sobrecarga del localizador de fila de datos ya se ha tenido en cuenta en el Paso 1.3, por lo que no es necesario efectuar ninguna modificación adicional. Vaya al paso siguiente.  
  
     Si el índice no clúster es único, el localizador de fila de datos debe tenerse en cuenta en todas las filas del nivel hoja.  
  
     Si el índice no clúster se encuentra sobre un montón, el localizador de fila de datos es el RID del montón (tamaño 8 bytes).  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + 1  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + 1  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + 8  
  
     Si el índice no clúster se encuentra sobre un índice clúster, el localizador de fila de datos es la clave de agrupación en clústeres. Las columnas que se deben combinar con la clave de índice no clúster son las columnas de la clave de agrupación en clústeres que ya no están presentes en el conjunto de columnas de clave de índice no clúster.  
  
     ***Num_Leaf_Cols***  = ***Num_Leaf_Cols*** + número de columnas de clave de agrupación en clústeres no presentes en el conjunto de columnas de clave de índice no agrupado (+ 1 si el índice agrupado no es único)  
  
     ***Fixed_Leaf_Size***  = ***Fixed_Leaf_Size*** + número de columnas de clave de agrupación en clústeres de longitud fija que no están presentes en el conjunto de columnas de clave de índice no agrupado  
  
     ***Num_Variable_Leaf_Cols***  = ***Num_Variable_Leaf_Cols*** + número de columnas de clave de agrupación en clústeres de longitud variable no presentes en el conjunto de columnas de clave de índice no agrupado (+ 1 si el índice agrupado no es único)  
  
     ***Max_Var_Leaf_Size***  = ***Max_Var_Leaf_Size*** + tamaño en bytes de las columnas de clave de agrupación en clústeres de longitud variable que no están presentes en el conjunto de columnas de clave de índice no agrupado (+ 4 si el índice agrupado no es único)  
  
3.  Calcule el tamaño del mapa de bits de valor NULL:  
  
     ***Leaf_Null_Bitmap***  = 2 + ((***Num_Leaf_Cols*** + 7) / 8)  
  
     Solamente debe utilizarse la parte entera de la expresión anterior. Descarte el resto.  
  
4.  Calcule el tamaño de los datos de longitud variable:  
  
     Si hay columnas de longitud variable en la clave de índice, incluidas las columnas de clave de agrupación en clústeres necesarias según se describe en el Paso 2.2, determine cuánto espacio se utiliza para almacenar las columnas de la fila de índice:  
  
     ***Variable_Leaf_Size***  = 2 + (***Num_Variable_Leaf_Cols*** x 2) + ***Max_Var_Leaf_Size***  
  
     Los bytes agregados a ***Max_Var_Key_Size*** son para el seguimiento de cada columna de longitud variable. En esta fórmula se supone que todas las columnas de longitud variable están llenas al 100 %. Si prevé que va a usarse un porcentaje inferior del espacio de almacenamiento de las columnas de longitud variable, puede ajustar el valor de ***Max_Var_Leaf_Size*** en función de ese porcentaje para obtener una estimación más precisa del tamaño global de la tabla.  
  
     Si no hay columnas de longitud variable, establezca ***Variable_Leaf_Size*** en 0.  
  
5.  Calcule el tamaño de la fila del índice:  
  
     ***Leaf_Row_Size***  = ***Fixed_Leaf_Size*** + ***Variable_Leaf_Size*** + ***Leaf_Null_Bitmap*** + 1 (para la sobrecarga de encabezado de una fila de índice) + 6 (para el puntero de identificador de página secundaria)  
  
6.  Calcule el número de filas de índice por página (8.096 bytes disponibles por página):  
  
     ***Leaf_Rows_Per_Page***  = 8096 / (***Leaf_Row_Size*** + 2)  
  
     Dado que las filas de índice no abarcan varias páginas, el número de filas de índice por página debe redondearse hacia abajo a la fila completa más cercana. El valor 2 de la fórmula representa la entrada de la fila en la matriz de zonas de la página.  
  
7.  Calcule el número de filas libres reservadas por página, basándose en el valor de [factor de relleno](../indexes/specify-fill-factor-for-an-index.md) especificado:  
  
     ***Free_Rows_Per_Page***  = 8096 x ((100 - ***Fill_Factor***) / 100) / (***Leaf_Row_Size*** + 2)  
  
     El factor de relleno que se utiliza en el cálculo es un valor entero y no un porcentaje. Dado que las filas no abarcan varias páginas, el número de filas por página debe redondearse hacia abajo a la fila completa más cercana. A medida que aumenta el factor de relleno, más datos se almacenan en cada página y menos páginas habrá. El valor 2 de la fórmula representa la entrada de la fila en la matriz de zonas de la página.  
  
8.  Calcule el número de páginas necesarias para almacenar todas las filas:  
  
     ***Num_Leaf_Pages***  = ***Num_Rows*** / (***Leaf_Rows_Per_Page*** - ***Free_Rows_Per_Page***)  
  
     El número de páginas estimado debe redondearse hacia arriba a la página completa más cercana.  
  
9. Calcule el tamaño del índice (8.192 bytes por página):  
  
     ***Leaf_Space_Used***  = 8192 x ***Num_Leaf_Pages***  
  
## <a name="step-3-calculate-the-space-used-to-store-index-information-in-the-non-leaf-levels"></a>Paso 3. Calcular el espacio utilizado para almacenar información del índice en los niveles no hoja  
 Siga estos pasos para estimar el espacio necesario para almacenar los niveles intermedio y raíz del índice. Para completar este paso, necesita los valores de los pasos 2 y 3.  
  
1.  Calcule el número de niveles no hoja del índice:  
  
     ***Los niveles no hoja*** = 1 + Index_Rows_Per_Page de registro (***Num_Leaf_Pages*** / ***Index_Rows_Per_Page***)  
  
     Redondee este valor al número entero más próximo. Este valor no incluye el nivel hoja del índice no clúster.  
  
2.  Calcule el número de páginas no hoja del índice:  
  
     ***Num_Index_Pages***  = ∑Level (***Num_Leaf_Pages/Index_Rows_Per_Page***<sup>Level</sup>)where 1 <= Level <= ***Levels***  
  
     Redondee cada sumando al número entero más próximo. Como ejemplo sencillo, considere un índice en el que ***Num_Leaf_Pages*** = 1000 e ***Index_Rows_Per_Page*** = 25. El primer nivel de índice por encima del nivel hoja almacena 1000 filas de índice, lo que equivale a una fila de índice por página hoja, y en cada página caben 25 filas de índice. Esto significa que se necesitan 40 páginas para almacenar las 1000 filas de índice. El siguiente nivel del índice debe almacenar 40 filas. Esto significa que necesita 2 páginas. El nivel final del índice debe almacenar 2 filas. Esto significa que necesita 1 página. Todo ello da lugar a 43 páginas no hoja de índice. Si se utilizan estos números en las fórmulas anteriores, el resultado será el siguiente:  
  
     ***Non-leaf_Levels*** = 1 + log25 (1000 / 25) = 3  
  
     ***Num_Index_Pages*** = 1000 /(25<sup>3</sup>) + 1000 / (25<sup>2</sup>) + 1000 / (25<sup>1</sup>) = 1 + 2 + 40 = 43, que es el número de páginas que se describe en el ejemplo.  
  
3.  Calcule el tamaño del índice (8.192 bytes por página):  
  
     ***Index_Space_Used***  = 8192 x ***Num_Index_Pages***  
  
## <a name="step-4-total-the-calculated-values"></a>Paso 4. Sumar los valores calculados  
 Sume los valores obtenidos en los dos pasos anteriores:  
  
 Tamaño del índice no agrupado (bytes) = ***Leaf_Space_Used*** + ***Index_Space_used***  
  
 En este cálculo no se tiene en cuenta lo siguiente:  
  
-   Particiones  
  
     La sobrecarga de espacio de la creación de particiones es mínima, pero resulta difícil de calcular. No es importante incluirla.  
  
-   Páginas de asignación  
  
     Se utiliza al menos una página IAM para realizar un seguimiento de las páginas asignadas a un montón, pero la sobrecarga de espacio es mínima y no existe ningún algoritmo para calcular de forma determinista el número exacto de páginas IAM que se utilizarán.  
  
-   Valores de objetos grandes (LOB)  
  
     El algoritmo para determinar exactamente la cantidad de espacio que se utilizará para almacenar los tipos de datos LOB y los valores `varchar(max)`, `varbinary(max)`, `nvarchar(max)`, `text`, `ntext`, `xml` y `image` es complejo. Basta con agregar el tamaño medio de los valores LOB esperados, multiplicarlo por ***Num_Rows***y sumar el resultado al tamaño total del índice no agrupado.  
  
-   Compresión  
  
     No se puede calcular previamente el tamaño de un índice comprimido.  
  
-   Columnas dispersas  
  
     Para obtener información sobre los requisitos de espacio de las columnas dispersas, vea [Use Sparse Columns](../tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Índices agrupados y no agrupados descritos](../indexes/clustered-and-nonclustered-indexes-described.md)   
 [Crear índices no clúster](../indexes/create-nonclustered-indexes.md)   
 [Crear índices clúster](../indexes/create-clustered-indexes.md)   
 [Calcular el tamaño de una tabla](estimate-the-size-of-a-table.md)   
 [Estimar el tamaño de un índice clúster](estimate-the-size-of-a-clustered-index.md)   
 [Estimar el tamaño de un montón](estimate-the-size-of-a-heap.md)   
 [Estimar el tamaño de una base de datos](estimate-the-size-of-a-database.md)  
  
  
