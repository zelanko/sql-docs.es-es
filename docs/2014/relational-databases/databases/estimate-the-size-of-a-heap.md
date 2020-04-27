---
title: Estimar el tamaño de un montón | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- disk space [SQL Server], indexes
- estimating heap size
- size [SQL Server], heap
- space [SQL Server], indexes
- heaps
ms.assetid: 81fd5ec9-ce0f-4c2c-8ba0-6c483cea6c75
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 80ba5505204f592ef04c939b3e84b6f3ca3c7c89
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62916749"
---
# <a name="estimate-the-size-of-a-heap"></a>Estimar el tamaño de un montón
  Los siguientes pasos pueden utilizarse para calcular el espacio necesario para almacenar datos en un montón:  
  
1.  Especifique el número de filas que habrá en la tabla:  
  
     ***Num_Rows***  = número de filas de la tabla  
  
2.  Especifique el número de columnas de longitud fija y de longitud variable, y calcule el espacio necesario para su almacenamiento:  
  
     Calcule el espacio que ocupa cada uno de estos grupos de columnas en la fila de datos. El tamaño de una columna depende del tipo y de la longitud especificados para los datos.  
  
     ***Num_Cols***  = número total de columnas (de longitud fija y variable)  
  
     ***Fixed_Data_Size***  = tamaño total en bytes de todas las columnas de longitud fija  
  
     ***Num_Variable_Cols***  = número de columnas de longitud variable  
  
     ***Max_Var_Size***  = tamaño máximo total en bytes de todas las columnas de longitud variable  
  
3.  Una parte de la fila, conocida como el mapa de bits NULL, se reserva para administrar la nulabilidad en las columnas. Calcule el tamaño:  
  
     ***Null_Bitmap***  = 2 + ((***Num_Cols*** + 7) / 8)  
  
     Solo debe utilizarse la parte entera de la expresión anterior. Descarte el resto.  
  
4.  Calcule el tamaño de los datos de longitud variable:  
  
     Si hay columnas de longitud variable en la tabla, determine cuánto espacio se utiliza para almacenar las columnas en la fila:  
  
     ***Variable_Data_Size***  = 2 + (***Num_Variable_Cols*** x 2) + ***Max_Var_Size***  
  
     Los bytes agregados a ***Max_Var_Size*** son para el seguimiento de cada columna de longitud variable. En esta fórmula se supone que todas las columnas de longitud variable están llenas al 100%. Si prevé que se va a usar un porcentaje inferior del espacio de almacenamiento de columnas de longitud variable, puede ajustar el valor de ***Max_Var_Size*** en función de ese porcentaje para obtener una estimación más precisa del tamaño global de la tabla.  
  
    > [!NOTE]  
    >  Puede combinar las columnas `varchar`, `nvarchar`, `varbinary` o `sql_variant` que hagan que el ancho total definido para la tabla sea superior a 8.060 bytes. La longitud de cada una de estas columnas todavía debe estar comprendida en el límite de 8.000 bytes para `varchar`una `nvarchar,``varbinary`columna, `sql_variant` o. Sin embargo, el ancho combinado puede superar el límite de 8.060 bytes de una tabla.  
  
     Si no hay columnas de longitud variable, establezca ***Variable_Data_Size*** en 0.  
  
5.  Calcule el tamaño total de la fila:  
  
     ***Row_Size***  = ***Fixed_Data_Size***Fixed_Data_Size + ***Variable_Data_Size***Variable_Data_Size + ***Null_Bitmap*** + 4  
  
     El valor 4 de la fórmula representa la sobrecarga del encabezado de la fila de datos.  
  
6.  Calcule el número de filas por página (8096 bytes libres por página):  
  
     ***Rows_Per_Page***  = 8096 / (***Row_Size*** + 2)  
  
     Dado que las filas no abarcan varias páginas, el número de filas por página debe redondearse hacia abajo a la fila completa más cercana. El valor 2 de la fórmula representa la entrada de la fila en la matriz de zonas de la página.  
  
7.  Calcule el número de páginas necesarias para almacenar todas las filas:  
  
     ***Num_Pages***  = ***Num_Rows*** / ***Rows_Per_Page***  
  
     El número de páginas estimado debe redondearse hacia arriba a la página completa más cercana.  
  
8.  Calcule el espacio necesario para almacenar los datos en el montón (8192 bytes en total por página):  
  
     Tamaño del montón (bytes) = 8192 x ***Num_Pages***  
  
 En este cálculo no se tiene en cuenta lo siguiente:  
  
-   Creación de particiones  
  
     La sobrecarga de espacio de la creación de particiones es mínima, pero resulta difícil de calcular. No es importante incluirla.  
  
-   Páginas de asignación  
  
     Se utiliza al menos una página IAM para realizar un seguimiento de las páginas asignadas a un montón, pero la sobrecarga de espacio es mínima y no existe ningún algoritmo para calcular de forma determinista el número exacto de páginas IAM que se utilizarán.  
  
-   Valores de objetos grandes (LOB)  
  
     El algoritmo para determinar exactamente la cantidad de espacio que se utilizará para almacenar los tipos `varchar(max)`de `varbinary(max)`datos `nvarchar(max)`LOB `text`,,,, `image` **ntextxml**y los valores es complejo. Basta con agregar solamente el tamaño medio de los valores de LOB que se esperan y agregarlo al tamaño total del montón.  
  
-   Compresión  
  
     No se puede calcular previamente el tamaño de un montón comprimido.  
  
-   Columnas dispersas  
  
     Para obtener información sobre los requisitos de espacio de las columnas dispersas, vea [Use Sparse Columns](../tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Consulte también  
 [Montones &#40;tablas sin índices agrupados&#41;](../indexes/heaps-tables-without-clustered-indexes.md)   
 [Índices agrupados y no agrupados descritos](../indexes/clustered-and-nonclustered-indexes-described.md)   
 [Crear índices clúster](../indexes/create-clustered-indexes.md)   
 [Crear índices no clúster](../indexes/create-nonclustered-indexes.md)   
 [Calcular el tamaño de una tabla](estimate-the-size-of-a-table.md)   
 [Estimar el tamaño de un índice agrupado](estimate-the-size-of-a-clustered-index.md)   
 [Estimar el tamaño de un índice no clúster](estimate-the-size-of-a-nonclustered-index.md)   
 [Estimar el tamaño de una base de datos](estimate-the-size-of-a-database.md)  
  
  
