---
title: Estimar el tamaño de un índice agrupado | Microsoft Docs
description: Siga este procedimiento para estimar la cantidad de espacio necesario para almacenar datos en un índice agrupado en SQL Server.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine, sql-database
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- space allocation [SQL Server], index size
- size [SQL Server], tables
- disk space [SQL Server], indexes
- predicting table size [SQL Server]
- table size [SQL Server]
- estimating table size
- space [SQL Server], indexes
- clustered indexes, table size
- nonclustered indexes [SQL Server], table size
- designing databases [SQL Server], estimating size
- calculating table size
ms.assetid: 2b5137f8-98ad-46b5-9aae-4c980259bf8d
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || >= sql-server-2016
ms.openlocfilehash: d963a8745d83be039fa2970a24d04a2a882bf7a9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97478366"
---
# <a name="estimate-the-size-of-a-clustered-index"></a>Estimar el tamaño de un índice clúster

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Los siguientes pasos pueden utilizarse para calcular el espacio necesario para almacenar datos en un índice clúster:  
  
1.  Calcule el espacio utilizado para almacenar datos en el nivel hoja del índice clúster.  
  
2.  Calcule el espacio utilizado para almacenar información del índice clúster.  
  
3.  Sumar los valores calculados.  
  
## <a name="step-1-calculate-the-space-used-to-store-data-in-the-leaf-level"></a>Paso 1. Calcular el espacio utilizado para almacenar datos en el nivel hoja  
  
1.  Especifique el número de filas que habrá en la tabla:  
  
     ***Num_Rows** _  = número de filas de la tabla  
  
2.  Especifique el número de columnas de longitud fija y de longitud variable, y calcule el espacio necesario para su almacenamiento:  
  
     Calcule el espacio que ocupa cada uno de estos grupos de columnas en la fila de datos. El tamaño de una columna depende del tipo y de la longitud especificados para los datos.  
  
     _*_Num_Cols_*_  = número total de columnas (de longitud fija y variable)  
  
     _*_Fixed_Data_Size_*_  = tamaño total en bytes de todas las columnas de longitud fija  
  
     _*_Num_Variable_Cols_*_  = número de columnas de longitud variable  
  
     _*_Max_Var_Size_*_  = tamaño máximo en bytes de todas las columnas de longitud variable  
  
3.  Si el índice agrupado no es único, tenga en cuenta la columna de _valor de unicidad*:  
  
     La columna de valor de unicidad es una columna de longitud variable que admite valores NULL. No será NULL y tendrá 4 bytes de tamaño en filas que tienen valores de clave no únicos. Este valor forma parte de la clave de índice y es necesario para asegurarse de que cada fila tiene un valor de clave único.  
  
     ***Num_Cols** _  = _*_Num_Cols_*_ + 1  
  
     _*_Num_Variable_Cols_*_  = _*_Num_Variable_Cols_*_ + 1  
  
     _*_Max_Var_Size_*_  = _*_Max_Var_Size_*_ + 4  
  
     Estas modificaciones presuponen que todos los valores no serán únicos.  
  
4.  Una parte de la fila, conocida como el mapa de bits NULL, se reserva para administrar la nulabilidad en las columnas. Calcule el tamaño:  
  
     _*_Null_Bitmap_*_  = 2 + ((_*_Num_Cols_*_ + 7) / 8)  
  
     Solo debe utilizarse la parte entera de la expresión anterior; descarte el resto.  
  
5.  Calcule el tamaño de los datos de longitud variable:  
  
     Si hay columnas de longitud variable en la tabla, determine cuánto espacio se utiliza para almacenar las columnas en la fila:  
  
     _*_Variable_Data_Size_*_  = 2 + (_*_Num_Variable_Cols_*_ x 2) + _*_Max_Var_Size_*_  
  
     Los bytes agregados a _*_Max_Var_Size_*_ son para el seguimiento de cada columna de longitud variable. En esta fórmula se supone que todas las columnas de longitud variable están llenas al 100%. Si prevé que se va a usar un porcentaje inferior del espacio de almacenamiento de columnas de longitud variable, puede ajustar el valor _*_Max_Var_Size_*_ en función de ese porcentaje para obtener una estimación más precisa del tamaño global de la tabla.  
  
    > [!NOTE]  
    >  Puede combinar las columnas _*varchar**, **nvarchar**, **varbinary** o **sql_variant** que hacen que el ancho total definido para la tabla sea superior a 8060 bytes. La longitud de cada una de estas columnas debe ajustarse al límite de 8000 bytes en columnas **varchar**, **varbinary** o **sql_variant** y de 4000 bytes en columnas **nvarchar** . Sin embargo, el ancho combinado puede superar el límite de 8.060 bytes de una tabla.  
  
     Si no hay columnas de longitud variable, establezca **_Variable_Data_Size_* _ en 0.  
  
6.  Calcule el tamaño total de la fila:  
  
     _*_Row_Size_*_  = _*_Fixed_Data_Size_*_ + _*_Variable_Data_Size_*_ + _*_Null_Bitmap_*_ + 4  
  
     El valor 4 representa la sobrecarga del encabezado de una fila de datos.  
  
7.  Calcule el número de filas por página (8096 bytes libres por página):  
  
     _*_Rows_Per_Page_*_  = 8096 / (_*_Row_Size_*_ + 2)  
  
     Dado que las filas no abarcan varias páginas, el número de filas por página debe redondearse hacia abajo a la fila completa más cercana. El valor 2 de la fórmula representa la entrada de la fila en la matriz de zonas de la página.  
  
8.  Calcule el número de filas libres reservadas por página, basándose en el valor de [factor de relleno](../../relational-databases/indexes/specify-fill-factor-for-an-index.md) especificado:  
  
     _*_Free_Rows_Per_Page_*_  = 8096 x ((100 - _*_Fill_Factor_*_) / 100) / (_*_Row_Size_*_ + 2)  
  
     El factor de relleno que se utiliza en el cálculo es un valor entero y no un porcentaje. Dado que las filas no abarcan varias páginas, el número de filas por página debe redondearse hacia abajo a la fila completa más cercana. A medida que aumenta el factor de relleno, más datos se almacenan en cada página y menos páginas habrá. El valor 2 de la fórmula representa la entrada de la fila en la matriz de zonas de la página.  
  
9. Calcule el número de páginas necesarias para almacenar todas las filas:  
  
     _*_Num_Leaf_Pages_*_  = _*_Num_Rows_*_ / (_*_Rows_Per_Page_*_ - _*_Free_Rows_Per_Page_*_ )  
  
     El número de páginas estimado debe redondearse hacia arriba a la página completa más cercana.  
  
10. Calcule la cantidad de espacio necesario para almacenar los datos en el nivel hoja (8.192 bytes por página):  
  
     _*_Leaf_space_used_*_  = 8192 x _*_Num_Leaf_Pages_*_  
  
## <a name="step-2-calculate-the-space-used-to-store-index-information"></a>Paso 2. Calcular el espacio utilizado para almacenar información de índice  
 Los siguientes pasos pueden utilizarse para calcular el espacio necesario para almacenar los niveles superiores del índice:  
  
1.  Especifique el número de columnas de longitud fija y variable de la clave de índice, y calcule el espacio necesario para su almacenamiento:  
  
     Las columnas de clave de un índice pueden incluir columnas de longitud fija y de longitud variable. Para estimar el tamaño de las filas de índice de nivel interior, calcule el espacio que ocupa cada uno de estos grupos de columnas en la fila de índice. El tamaño de una columna depende del tipo y de la longitud especificados para los datos.  
  
     _*_Num_Key_Cols_*_  = número total de columnas de clave (de longitud fija y variable)  
  
     _*_Fixed_Key_Size_*_  = tamaño total en bytes de todas las columnas de clave de longitud fija  
  
     _*_Num_Variable_Key_Cols_*_  = número de columnas de clave de longitud variable  
  
     _*_Max_Var_Key_Size_*_  = tamaño máximo en bytes de todas las columnas de clave de longitud variable  
  
2.  Tenga en cuenta cualquier columna de valor de unicidad si el índice no es único:  
  
     La columna de valor de unicidad es una columna de longitud variable que admite valores NULL. No será NULL y tendrá 4 bytes de tamaño en filas que tienen valores de clave de índice no únicos. Este valor forma parte de la clave de índice y es necesario para asegurarse de que cada fila tiene un valor de clave único.  
  
     _*_Num_Key_Cols_*_  = _*_Num_Key_Cols_*_ + 1  
  
     _*_Num_Variable_Key_Cols_*_  = _*_Num_Variable_Key_Cols_*_ + 1  
  
     _*_Max_Var_Key_Size_*_  = _*_Max_Var_Key_Size_*_ + 4  
  
     Estas modificaciones presuponen que todos los valores no serán únicos.  
  
3.  Calcule el tamaño del mapa de bits de valor NULL:  
  
     Si hay columnas que admiten valores NULL en la clave de índice, una parte de la fila de índice se reserva para el mapa de bits NULL. Calcule el tamaño:  
  
     _*_Index_Null_Bitmap_*_  = 2 + ((número de columnas de la fila de índice + 7) / 8)  
  
     Solamente debe utilizarse la parte entera de la expresión anterior. Descarte el resto.  
  
     Si no existen columnas de clave que aceptan valores NULL, establezca _*_Index_Null_Bitmap_*_ en 0.  
  
4.  Calcule el tamaño de los datos de longitud variable:  
  
     Si hay columnas de longitud variable en el índice, determine cuánto espacio se utiliza para almacenar las columnas en la fila de índice:  
  
     _*_Variable_Key_Size_*_  = 2 + (_*_Num_Variable_Key_Cols_*_ x 2) + _*_Max_Var_Key_Size_*_  
  
     Los bytes agregados a _*_Max_Var_Key_Size_*_ son para el seguimiento de cada columna de longitud variable. En esta fórmula se supone que todas las columnas de longitud variable están llenas al 100%. Si prevé que se va a usar un porcentaje inferior del espacio de almacenamiento de columnas de longitud variable, puede ajustar el valor de _*_Max_Var_Key_Size_*_ en función de ese porcentaje para obtener una estimación más precisa del tamaño global de la tabla.  
  
     Si no hay columnas de longitud variable, establezca _*_Variable_Key_Size_*_ en 0.  
  
5.  Calcule el tamaño de la fila del índice:  
  
     _*_Index_Row_Size_*_  = _*_Fixed_Key_Size_*_ + _*_Variable_Key_Size_*_ + _*_Index_Null_Bitmap_*_ + 1 (para la sobrecarga de encabezado de una fila de índice) + 6 (para el puntero de identificador de página secundaria)  
  
6.  Calcule el número de filas de índice por página (8.096 bytes disponibles por página):  
  
     _*_Index_Rows_Per_Page_*_  = 8096 / (_*_Index_Row_Size_*_ + 2)  
  
     Dado que las filas de índice no abarcan varias páginas, el número de filas de índice por página debe redondearse hacia abajo a la fila completa más cercana. El valor 2 de la fórmula representa la entrada de la fila en la matriz de zonas de la página.  
  
7.  Calcule el número de niveles del índice:  
  
     _*_Non-leaf_Levels_*_  = 1 + log (Index_Rows_Per_Page) (_*_Num_Leaf_Pages_*_ / _*_Index_Rows_Per_Page_*_)  
  
     Redondee este valor al número entero más próximo. Este valor no incluye el nivel hoja del índice clúster.  
  
8.  Calcule el número de páginas no hoja del índice:  
  
     _*_Num_Index_Pages =_*_ ∑Level _*_ (Num_Leaf_Pages / (Index_Rows_Per_Page_ *_^Level_* _))_ *_  
  
     donde 1 <= Level <= _*_Non-leaf_Levels_*_  
  
     Redondee cada sumando al número entero más próximo. Como ejemplo sencillo, considere un índice en el que _*_Num_Leaf_Pages_*_ = 1000 e _*_Index_Rows_Per_Page_*_ = 25. El primer nivel de índice por encima del nivel hoja almacena 1000 filas de índice, lo que equivale a una fila de índice por página hoja, y en cada página caben 25 filas de índice. Esto significa que se necesitan 40 páginas para almacenar las 1000 filas de índice. El siguiente nivel del índice debe almacenar 40 filas. Esto significa que necesita 2 páginas. El nivel final del índice debe almacenar 2 filas. Esto significa que necesita 1 página. Todo ello supone 43 páginas de índice no hoja. Si se utilizan estos números en las fórmulas anteriores, el resultado será el siguiente:  
  
     _*_Non-leaf_Levels_*_  = 1 + log(25) (1000 / 25) = 3  
  
     _*_Num_Index_Pages_*_ = 1000/(25^3)+ 1000/(25^2) + 1000/(25^1) = 1 + 2 + 40 = 43, que es el número de páginas que se describe en el ejemplo.  
  
9. Calcule el tamaño del índice (8.192 bytes por página):  
  
     _*_Index_Space_Used_*_  = 8192 x _*_Num_Index_Pages_*_  
  
## <a name="step-3-total-the-calculated-values"></a>Paso 3. Sumar los valores calculados  
 Sume los valores obtenidos en los dos pasos anteriores:  
  
 Tamaño del índice agrupado (bytes) = _*_Leaf_Space_Used_*_ + _*_Index_Space_used_*_  
  
 En este cálculo no se tiene en cuenta lo siguiente:  
  
-   Creación de particiones  
  
     La sobrecarga de espacio de la creación de particiones es mínima, pero resulta difícil de calcular. No es importante incluirla.  
  
-   Páginas de asignación  
  
     Se utiliza al menos una página IAM para realizar un seguimiento de las páginas asignadas a un montón, pero la sobrecarga de espacio es mínima y no existe ningún algoritmo para calcular de forma determinista el número exacto de páginas IAM que se utilizarán.  
  
-   Valores de objetos grandes (LOB)  
  
     El algoritmo para determinar exactamente la cantidad de espacio que se usará para almacenar los tipos de datos LOB y los valores _*varchar(max)**, **varbinary(max)** , **nvarchar(max)** , **text**, **ntext**, **xml** e **image** es complejo. Basta con agregar el tamaño medio de los valores LOB que se esperan, multiplicarlo por **_Num_Rows_**, y agregarlo al tamaño total del índice agrupado.  
  
-   Compresión  
  
     No se puede calcular previamente el tamaño de un índice comprimido.  
  
-   Columnas dispersas  
  
     Para obtener información sobre los requisitos de espacio de las columnas dispersas, vea [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Consulte también  
 [Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [Calcular el tamaño de una tabla](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [Crear índices clúster](../../relational-databases/indexes/create-clustered-indexes.md)   
 [Crear índices no clúster](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [Estimar el tamaño de un índice no clúster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)   
 [Estimar el tamaño de un montón](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [Estimar el tamaño de una base de datos](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
