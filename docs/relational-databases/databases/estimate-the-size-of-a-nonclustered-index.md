---
title: Estimar el tamaño de un índice no agrupado | Microsoft Docs
description: Use este procedimiento a fin de estimar la cantidad de espacio necesario para almacenar un índice no agrupado en SQL Server.
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine, sql-database
ms.technology: supportability
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
monikerRange: = azuresqldb-current || >= sql-server-2016
ms.openlocfilehash: 9c234bb8371d99025bd97cfb86f5d85472d34ee4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474086"
---
# <a name="estimate-the-size-of-a-nonclustered-index"></a>Estimar el tamaño de un índice no clúster

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Siga estos pasos para estimar el espacio necesario para almacenar un índice no clúster:  
  
1.  Calcular las variables que deben usarse en los pasos 2 y 3.  
  
2.  Calcular el espacio utilizado para almacenar información del índice en el nivel hoja del índice no clúster.  
  
3.  Calcular el espacio utilizado para almacenar información del índice en los niveles no hoja del índice no clúster.  
  
4.  Sumar los valores calculados.  
  
## <a name="step-1-calculate-variables-for-use-in-steps-2-and-3"></a>Paso 1. Calcularlas variables que deben usarse en los pasos 2 y 3  
 Los siguientes pasos pueden utilizarse para calcular las variables que se utilizan para estimar el espacio necesario para almacenar los niveles superiores del índice:  
  
1.  Especifique el número de filas que habrá en la tabla:  
  
     ***Num_Rows** _  = número de filas de la tabla  
  
2.  Especifique el número de columnas de longitud fija y variable de la clave de índice, y calcule el espacio necesario para su almacenamiento:  
  
     Las columnas de clave de un índice pueden incluir columnas de longitud fija y de longitud variable. Para estimar el tamaño de las filas de índice de nivel interior, calcule el espacio que ocupa cada uno de estos grupos de columnas en la fila de índice. El tamaño de una columna depende del tipo y de la longitud especificados para los datos.  
  
     _*_Num_Key_Cols_*_  = número total de columnas de clave (de longitud fija y variable)  
  
     _*_Fixed_Key_Size_*_  = tamaño total en bytes de todas las columnas de clave de longitud fija  
  
     _*_Num_Variable_Key_Cols_*_  = número de columnas de clave de longitud variable  
  
     _*_Max_Var_Key_Size_*_  = tamaño máximo en bytes de todas las columnas de clave de longitud variable  
  
3.  Tenga en cuenta el localizador de fila de datos necesario si el índice no es único:  
  
     Si el índice no clúster no es único, el localizador de fila de datos se combina con la clave de índice no clúster para generar un valor de clave único para cada fila.  
  
     Si el índice no clúster se encuentra sobre un montón, el localizador de fila de datos es el RID del montón. Tiene un tamaño de 8 bytes.  
  
     _*_Num_Key_Cols_*_  = _*_Num_Key_Cols_*_ + 1  
  
     _*_Num_Variable_Key_Cols_*_  = _*_Num_Variable_Key_Cols_*_ + 1  
  
     _*_Max_Var_Key_Size_*_  = _*_Max_Var_Key_Size_*_ + 8  
  
     Si el índice no clúster se encuentra sobre un índice clúster, el localizador de fila de datos es la clave de agrupación en clústeres. Las columnas que se deben combinar con la clave de índice no clúster son las columnas de la clave de agrupación en clústeres que ya no están presentes en el conjunto de columnas de clave de índice no clúster.  
  
     _*_Num_Key_Cols_*_  = _*_Num_Key_Cols_*_ + número de columnas de clave de agrupación en clústeres no presentes en el conjunto de columnas de clave de índice no agrupado (+ 1 si el índice agrupado no es único)  
  
     _*_Fixed_Key_Size_*_  = _*_Fixed_Key_Size_*_ + tamaño total en bytes de las columnas de clave de agrupación en clústeres de longitud fija que no están presentes en el conjunto de columnas de clave de índice no agrupado  
  
     _*_Num_Variable_Key_Cols_*_  = _*_Num_Variable_Key_Cols_*_ + número de columnas de clave de agrupación en clústeres de longitud variable no presentes en el conjunto de columnas de clave de índice no agrupado (+ 1 si el índice agrupado no es único)  
  
     _*_Max_Var_Key_Size_*_  = _*_Max_Var_Key_Size_*_ + tamaño máximo en bytes de las columnas de clave de agrupación en clústeres de longitud variable no presentes en el conjunto de columnas de clave de índice no agrupado (+ 4 si el índice agrupado no es único)  
  
4.  Se puede reservar parte de la fila, conocida como el mapa de bits NULL, para administrar la nulabilidad de las columnas. Calcule el tamaño:  
  
     Si existen columnas que aceptan valores NULL en la clave del índice, incluidas las columnas de clave de agrupación en clústeres necesarias que se describen en el paso 1.3, se reserva parte de la fila de índice para el mapa de bits NULL.  
  
     _*_Index_Null_Bitmap_*_  = 2 + ((número de columnas de la fila de índice + 7) / 8)  
  
     Solamente debe utilizarse la parte entera de la expresión anterior. Descarte el resto.  
  
     Si no existen columnas de clave que aceptan valores NULL, establezca _*_Index_Null_Bitmap_*_ en 0.  
  
5.  Calcule el tamaño de los datos de longitud variable:  
  
     Si hay columnas de longitud variable en la clave de índice, incluidas las columnas de clave de índice clúster necesarias, determine cuánto espacio se utiliza para almacenar las columnas de la fila de índice:  
  
     _*_Variable_Key_Size_*_  = 2 + (_*_Num_Variable_Key_Cols_*_ x 2) + _*_Max_Var_Key_Size_*_  
  
     Los bytes agregados a _*_Max_Var_Key_Size_*_ son para el seguimiento de cada columna de longitud variable. En esta fórmula se supone que todas las columnas de longitud variable están llenas al 100 %. Si prevé que se va a usar un porcentaje inferior del espacio de almacenamiento de columnas de longitud variable, puede ajustar el valor de _*_Max_Var_Key_Size_*_ en función de ese porcentaje para obtener una estimación más precisa del tamaño global de la tabla.  
  
     Si no hay columnas de longitud variable, establezca _*_Variable_Key_Size_*_ en 0.  
  
6.  Calcule el tamaño de la fila del índice:  
  
     _*_Index_Row_Size_*_  = _*_Fixed_Key_Size_*_ + _*_Variable_Key_Size_*_ + _*_Index_Null_Bitmap_*_ + 1 (para la sobrecarga de encabezado de una fila de índice) + 6 (para el puntero de identificador de página secundaria)  
  
7.  Calcule el número de filas de índice por página (8.096 bytes disponibles por página):  
  
     _*_Index_Rows_Per_Page_*_  = 8096 / (_*_Index_Row_Size_*_ + 2)  
  
     Dado que las filas de índice no abarcan varias páginas, el número de filas de índice por página debe redondearse hacia abajo a la fila completa más cercana. El valor 2 de la fórmula representa la entrada de la fila en la matriz de zonas de la página.  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information-in-the-leaf-level"></a>Paso 2. Calcular el espacio utilizado para almacenar información del índice en el nivel hoja  
 Para estimar el espacio necesario para almacenar el nivel hoja del índice, puede utilizar los siguientes pasos. Para completar este paso, necesita los valores del Paso 1.  
  
1.  Especifique el número de columnas de longitud fija y variable en el nivel hoja y calcule el espacio necesario para su almacenamiento:  
  
    > [!NOTE]  
    >  Un índice no clúster se puede ampliar incluyendo columnas que no son de clave además de las columnas de clave de índice. Estas columnas adicionales solamente se almacenan en el nivel hoja del índice no clúster. Para más información, consulte [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
    > [!NOTE]  
    >  Puede combinar las columnas _*varchar**, **nvarchar**, **varbinary** o **sql_variant** que hacen que el ancho total definido para la tabla sea superior a 8060 bytes. La longitud de cada una de estas columnas debe ajustarse al límite de 8000 bytes en columnas **varchar**, **varbinary** o **sql_variant** y de 4000 bytes en columnas **nvarchar** . Sin embargo, el ancho combinado puede superar el límite de 8.060 bytes de una tabla. Esto también se aplica a filas de hoja de índice no clúster con columnas incluidas.  
  
     Si el índice no clúster no incluye columnas, utilice los valores del Paso 1, incluidas las modificaciones determinadas en el Paso 1.3:  
  
     **_Num_Leaf_Cols_* _  = _*_Num_Key_Cols_*_  
  
     _*_Fixed_Leaf_Size_*_  = _*_Fixed_Key_Size_*_  
  
     _*_Num_Variable_Leaf_Cols_*_  = _*_Num_Variable_Key_Cols_*_  
  
     _*_Max_Var_Leaf_Size_*_  = _*_Max_Var_Key_Size_*_  
  
     Si el índice no clúster no incluye columnas, agregue los valores apropiados a los valores del Paso 1, incluidas las modificaciones del Paso 1.3. El tamaño de una columna depende del tipo y de la longitud especificados para los datos. Para obtener más información, vea [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
     _*_Num_Leaf_Cols_*_  = _*_Num_Key_Cols_*_ + número de columnas incluidas  
  
     _*_Fixed_Leaf_Size_*_  = _*_Fixed_Key_Size_*_ + tamaño total de bytes de las columnas de longitud fija incluidas  
  
     _*_Num_Variable_Leaf_Cols_*_  = _*_Num_Variable_Key_Cols_*_ + número de columnas de longitud variable incluidas  
  
     _*_Max_Var_Leaf_Size_*_  = _*_Max_Var_Key_Size_*_ + tamaño máximo de bytes de todas las columnas de longitud variable incluidas  
  
2.  Tenga en cuenta el localizador de fila de datos:  
  
     Si el índice no clúster no es único, la sobrecarga del localizador de fila de datos ya se ha tenido en cuenta en el Paso 1.3, por lo que no es necesario efectuar ninguna modificación adicional. Vaya al paso siguiente.  
  
     Si el índice no clúster es único, el localizador de fila de datos debe tenerse en cuenta en todas las filas del nivel hoja.  
  
     Si el índice no clúster se encuentra sobre un montón, el localizador de fila de datos es el RID del montón (tamaño 8 bytes).  
  
     _*_Num_Leaf_Cols_*_  = _*_Num_Leaf_Cols_*_ + 1  
  
     _*_Num_Variable_Leaf_Cols_*_  = _*_Num_Variable_Leaf_Cols_*_ + 1  
  
     _*_Max_Var_Leaf_Size_*_  = _*_Max_Var_Leaf_Size_*_ + 8  
  
     Si el índice no clúster se encuentra sobre un índice clúster, el localizador de fila de datos es la clave de agrupación en clústeres. Las columnas que se deben combinar con la clave de índice no clúster son las columnas de la clave de agrupación en clústeres que ya no están presentes en el conjunto de columnas de clave de índice no clúster.  
  
     _*_Num_Leaf_Cols_*_  = _*_Num_Leaf_Cols_*_ + número de columnas de clave de agrupación en clústeres no presentes en el conjunto de columnas de clave de índice no agrupado (+ 1 si el índice agrupado no es único)  
  
     _*_Fixed_Leaf_Size_*_  = _*_Fixed_Leaf_Size_*_ + número de columnas de clave de agrupación en clústeres de longitud fija que no están presentes en el conjunto de columnas de clave de índice no agrupado  
  
     _*_Num_Variable_Leaf_Cols_*_  = _*_Num_Variable_Leaf_Cols_*_ + número de columnas de clave de agrupación en clústeres de longitud variable no presentes en el conjunto de columnas de clave de índice no agrupado (+ 1 si el índice agrupado no es único)  
  
     _*_Max_Var_Leaf_Size_*_  = _*_Max_Var_Leaf_Size_*_ + tamaño en bytes de las columnas de clave de agrupación en clústeres de longitud variable que no están presentes en el conjunto de columnas de clave de índice no agrupado (+ 4 si el índice agrupado no es único)  
  
3.  Calcule el tamaño del mapa de bits de valor NULL:  
  
     _*_Leaf_Null_Bitmap_*_  = 2 + ((_*_Num_Leaf_Cols_*_ + 7) / 8)  
  
     Solamente debe utilizarse la parte entera de la expresión anterior. Descarte el resto.  
  
4.  Calcule el tamaño de los datos de longitud variable:  
  
     Si hay columnas de longitud variable (columnas de clave o incluidas), incluidas las columnas de clave de agrupación en clústeres necesarias según se describe en el Paso 2.2, determine cuánto espacio se utiliza para almacenar las columnas de la fila de índice:  
  
     _*_Variable_Leaf_Size_*_  = 2 + (_*_Num_Variable_Leaf_Cols_*_ x 2) + _*_Max_Var_Leaf_Size_*_  
  
     Los bytes agregados a _*_Max_Var_Key_Size_*_ son para el seguimiento de cada columna de longitud variable. En esta fórmula se supone que todas las columnas de longitud variable están llenas al 100 %. Si prevé que va a usarse un porcentaje inferior del espacio de almacenamiento de las columnas de longitud variable, puede ajustar el valor de _*_Max_Var_Leaf_Size_*_ en función de ese porcentaje para obtener una estimación más precisa del tamaño global de la tabla.  
  
     Si no hay columnas de longitud variable (columnas de clave o incluidas), establezca _*_Variable_Leaf_Size_*_ en 0.  
  
5.  Calcule el tamaño de la fila del índice:  
  
     _*_Leaf_Row_Size_*_  = _*_Fixed_Leaf_Size_*_ + _*_Variable_Leaf_Size_*_ + _*_Leaf_Null_Bitmap_*_ + 1 (para la sobrecarga de encabezado de una fila de índice)  
  
6.  Calcule el número de filas de índice por página (8.096 bytes disponibles por página):  
  
     _*_Leaf_Rows_Per_Page_*_  = 8096 / (_*_Leaf_Row_Size_*_ + 2)  
  
     Dado que las filas de índice no abarcan varias páginas, el número de filas de índice por página debe redondearse hacia abajo a la fila completa más cercana. El valor 2 de la fórmula representa la entrada de la fila en la matriz de zonas de la página.  
  
7.  Calcule el número de filas libres reservadas por página, basándose en el valor de [factor de relleno](../../relational-databases/indexes/specify-fill-factor-for-an-index.md) especificado:  
  
     _*_Free_Rows_Per_Page_*_  = 8096 x ((100 - _*_Fill_Factor_*_) / 100) / (_*_Leaf_Row_Size_*_ + 2)  
  
     El factor de relleno que se utiliza en el cálculo es un valor entero y no un porcentaje. Dado que las filas no abarcan varias páginas, el número de filas por página debe redondearse hacia abajo a la fila completa más cercana. A medida que aumenta el factor de relleno, más datos se almacenan en cada página y menos páginas habrá. El valor 2 de la fórmula representa la entrada de la fila en la matriz de zonas de la página.  
  
8.  Calcule el número de páginas necesarias para almacenar todas las filas:  
  
     _*_Num_Leaf_Pages_*_  = _*_Num_Rows_*_ / (_*_Leaf_Rows_Per_Page_*_ - _*_Free_Rows_Per_Page_*_ )  
  
     El número de páginas estimado debe redondearse hacia arriba a la página completa más cercana.  
  
9. Calcule el tamaño del índice (8.192 bytes por página):  
  
     _*_Leaf_Space_Used_*_  = 8192 x _*_Num_Leaf_Pages_*_  
  
## <a name="step-3-calculate-the-space-used-to-store-index-information-in-the-non-leaf-levels"></a>Paso 3. Calcular el espacio utilizado para almacenar información del índice en los niveles no hoja  
 Siga estos pasos para estimar el espacio necesario para almacenar los niveles intermedio y raíz del índice. Para completar este paso, necesita los valores de los pasos 2 y 3.  
  
1.  Calcule el número de niveles no hoja del índice:  
  
     _*_Non-leaf Levels_*_  = 1 + log (Index_Rows_Per_Page) (_*_Num_Leaf_Pages_*_ / _*_Index_Rows_Per_Page_*_)  
  
     Redondee este valor al número entero más próximo. Este valor no incluye el nivel hoja del índice no clúster.  
  
2.  Calcule el número de páginas no hoja del índice:  
  
     _*_Num_Index_Pages_*_  = ∑Level (_*_Num_Leaf_Pages/Index_Rows_Per_Page_*_^Level) donde 1 <= Level <= _*_Levels_*_  
  
     Redondee cada sumando al número entero más próximo. Como ejemplo sencillo, considere un índice en el que _*_Num_Leaf_Pages_*_ = 1000 e _*_Index_Rows_Per_Page_*_ = 25. El primer nivel de índice por encima del nivel hoja almacena 1000 filas de índice, lo que equivale a una fila de índice por página hoja, y en cada página caben 25 filas de índice. Esto significa que se necesitan 40 páginas para almacenar las 1000 filas de índice. El siguiente nivel del índice debe almacenar 40 filas. Esto significa que necesita 2 páginas. El nivel final del índice debe almacenar 2 filas. Esto significa que necesita 1 página. Todo ello da lugar a 43 páginas no hoja de índice. Si se utilizan estos números en las fórmulas anteriores, el resultado será el siguiente:  
  
     _*_Non-leaf_Levels_*_  = 1 + log(25) (1000 / 25) = 3  
  
     _*_Num_Index_Pages_*_ = 1000/(25^3)+ 1000/(25^2) + 1000/(25^1) = 1 + 2 + 40 = 43, que es el número de páginas que se describe en el ejemplo.  
  
3.  Calcule el tamaño del índice (8.192 bytes por página):  
  
     _*_Index_Space_Used_*_  = 8192 x _*_Num_Index_Pages_*_  
  
## <a name="step-4-total-the-calculated-values"></a>Paso 4. Sumar los valores calculados  
 Sume los valores obtenidos en los dos pasos anteriores:  
  
 Tamaño del índice no agrupado (bytes) = _*_Leaf_Space_Used_*_ + _*_Index_Space_used_*_  
  
 En este cálculo no se tiene en cuenta lo siguiente:  
  
-   Creación de particiones  
  
     La sobrecarga de espacio de la creación de particiones es mínima, pero resulta difícil de calcular. No es importante incluirla.  
  
-   Páginas de asignación  
  
     Se utiliza al menos una página IAM para realizar un seguimiento de las páginas asignadas a un montón, pero la sobrecarga de espacio es mínima y no existe ningún algoritmo para calcular de forma determinista el número exacto de páginas IAM que se utilizarán.  
  
-   Valores de objetos grandes (LOB)  
  
     El algoritmo para determinar exactamente la cantidad de espacio que se usará para almacenar los tipos de datos LOB y los valores _*varchar(max)**, **varbinary(max)** , **nvarchar(max)** , **text**, **ntext**, **xml** e **image** es complejo. Basta con agregar el tamaño medio de los valores LOB esperados, multiplicarlo por **_Num_Rows_** y sumar el resultado al tamaño total del índice no agrupado.  
  
-   Compresión  
  
     No se puede calcular previamente el tamaño de un índice comprimido.  
  
-   Columnas dispersas  
  
     Para obtener información sobre los requisitos de espacio de las columnas dispersas, vea [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Consulte también  
 [Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [Crear índices no clúster](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [Crear índices clúster](../../relational-databases/indexes/create-clustered-indexes.md)   
 [Calcular el tamaño de una tabla](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [Estimar el tamaño de un índice agrupado](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Estimar el tamaño de un montón](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Estimar el tamaño de una base de datos](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
