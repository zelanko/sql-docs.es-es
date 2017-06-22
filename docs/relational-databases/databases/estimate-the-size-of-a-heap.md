---
title: "Estimar el tamaño de un montón | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- disk space [SQL Server], indexes
- estimating heap size
- size [SQL Server], heap
- space [SQL Server], indexes
- heaps
ms.assetid: 81fd5ec9-ce0f-4c2c-8ba0-6c483cea6c75
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 67e38d5ab97529fbd912361aa16fa96587173f3e
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

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
    >  Puede combinar las columnas **varchar**, **nvarchar**, **varbinary**o **sql_variant** que hacen que el ancho total definido para la tabla sea superior a 8060 bytes. La longitud de cada una de estas columnas debe ajustarse al límite de 8000 bytes en una columna **varchar**, **nvarchar,****varbinary**o **sql_variant** . Sin embargo, el ancho combinado puede superar el límite de 8.060 bytes de una tabla.  
  
     Si no hay columnas de longitud variable, establezca ***Variable_Data_Size*** en 0.  
  
5.  Calcule el tamaño total de la fila:  
  
     ***Row_Size***  = ***Fixed_Data_Size*** + ***Variable_Data_Size*** + ***Null_Bitmap*** + 4  
  
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
  
-   Particiones  
  
     La sobrecarga de espacio de la creación de particiones es mínima, pero resulta difícil de calcular. No es importante incluirla.  
  
-   Páginas de asignación  
  
     Se utiliza al menos una página IAM para realizar un seguimiento de las páginas asignadas a un montón, pero la sobrecarga de espacio es mínima y no existe ningún algoritmo para calcular de forma determinista el número exacto de páginas IAM que se utilizarán.  
  
-   Valores de objetos grandes (LOB)  
  
     El algoritmo para determinar exactamente la cantidad de espacio que se usará para almacenar los tipos de datos LOB y los valores **varchar(max)**, **varbinary(max)**, **nvarchar(max)**, **text**, **ntextxml**e **image** es complejo. Basta con agregar solamente el tamaño medio de los valores de LOB que se esperan y agregarlo al tamaño total del montón.  
  
-   Compresión  
  
     No se puede calcular previamente el tamaño de un montón comprimido.  
  
-   Columnas dispersas  
  
     Para obtener información sobre los requisitos de espacio de las columnas dispersas, vea [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Montones &#40;tablas sin índices agrupados&#41;](../../relational-databases/indexes/heaps-tables-without-clustered-indexes.md)   
 [Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [Crear índices clúster](../../relational-databases/indexes/create-clustered-indexes.md)   
 [Crear índices no clúster](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [Calcular el tamaño de una tabla](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [Estimar el tamaño de un índice clúster](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Estimar el tamaño de un índice no clúster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)   
 [Estimar el tamaño de una base de datos](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
