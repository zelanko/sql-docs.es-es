---
title: Estimar el tamaño de un montón | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f57b07be679195794df5f0f9fe2329417a0b30f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62860691"
---
# <a name="estimate-the-size-of-a-heap"></a>Estimar el tamaño de un montón
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Los siguientes pasos pueden utilizarse para calcular el espacio necesario para almacenar datos en un montón:  
  
1.  Especifique el número de filas que habrá en la tabla:  
  
     **_Num_Rows_**  = número de filas de la tabla  
  
2.  Especifique el número de columnas de longitud fija y de longitud variable, y calcule el espacio necesario para su almacenamiento:  
  
     Calcule el espacio que ocupa cada uno de estos grupos de columnas en la fila de datos. El tamaño de una columna depende del tipo y de la longitud especificados para los datos.  
  
     **_Num_Cols_**  = número total de columnas (de longitud fija y variable)  
  
     **_Fixed_Data_Size_**  = tamaño total en bytes de todas las columnas de longitud fija  
  
     **_Num_Variable_Cols_**  = número de columnas de longitud variable  
  
     **_Max_Var_Size_**  = tamaño máximo total en bytes de todas las columnas de longitud variable  
  
3.  Una parte de la fila, conocida como el mapa de bits NULL, se reserva para administrar la nulabilidad en las columnas. Calcule el tamaño:  
  
     **_Null_Bitmap_**  = 2 + (( **_Num_Cols_** + 7) / 8)  
  
     Solo debe utilizarse la parte entera de la expresión anterior. Descarte el resto.  
  
4.  Calcule el tamaño de los datos de longitud variable:  
  
     Si hay columnas de longitud variable en la tabla, determine cuánto espacio se utiliza para almacenar las columnas en la fila:  
  
     **_Variable_Data_Size_**  = 2 + ( **_Num_Variable_Cols_** x 2) + **_Max_Var_Size_**  
  
     Los bytes agregados a **_Max_Var_Size_** son para el seguimiento de cada columna de longitud variable. En esta fórmula se supone que todas las columnas de longitud variable están llenas al 100%. Si prevé que se va a usar un porcentaje inferior del espacio de almacenamiento de columnas de longitud variable, puede ajustar el valor de **_Max_Var_Size_** en función de ese porcentaje para obtener una estimación más precisa del tamaño global de la tabla.  
  
    > [!NOTE]  
    >  Puede combinar las columnas **varchar**, **nvarchar**, **varbinary**o **sql_variant** que hacen que el ancho total definido para la tabla sea superior a 8060 bytes. La longitud de cada una de estas columnas debe ajustarse al límite de 8.000 bytes en una columna **varchar**, **nvarchar, varbinary** o **sql_variant**. Sin embargo, el ancho combinado puede superar el límite de 8.060 bytes de una tabla.  
  
     Si no hay columnas de longitud variable, establezca **_Variable_Data_Size_** en 0.  
  
5.  Calcule el tamaño total de la fila:  
  
     **_Row_Size_**   =  **_Fixed_Data_Size_**  +  **_Variable_Data_Size_**  +  **_Null_Bitmap_** + 4  
  
     El valor 4 de la fórmula representa la sobrecarga del encabezado de la fila de datos.  
  
6.  Calcule el número de filas por página (8096 bytes libres por página):  
  
     **_Rows_Per_Page_**  = 8096 / ( **_Row_Size_** + 2)  
  
     Dado que las filas no abarcan varias páginas, el número de filas por página debe redondearse hacia abajo a la fila completa más cercana. El valor 2 de la fórmula representa la entrada de la fila en la matriz de zonas de la página.  
  
7.  Calcule el número de páginas necesarias para almacenar todas las filas:  
  
     **_Num_Pages_**   =  **_Num_Rows_**  /  **_Rows_Per_Page_**  
  
     El número de páginas estimado debe redondearse hacia arriba a la página completa más cercana.  
  
8.  Calcule el espacio necesario para almacenar los datos en el montón (8192 bytes en total por página):  
  
     Tamaño del montón (bytes) = 8192 x **_Num_Pages_**  
  
 En este cálculo no se tiene en cuenta lo siguiente:  
  
-   Particiones  
  
     La sobrecarga de espacio de la creación de particiones es mínima, pero resulta difícil de calcular. No es importante incluirla.  
  
-   Páginas de asignación  
  
     Se utiliza al menos una página IAM para realizar un seguimiento de las páginas asignadas a un montón, pero la sobrecarga de espacio es mínima y no existe ningún algoritmo para calcular de forma determinista el número exacto de páginas IAM que se utilizarán.  
  
-   Valores de objetos grandes (LOB)  
  
     El algoritmo para determinar exactamente la cantidad de espacio que se usará para almacenar los tipos de datos LOB y los valores **varchar(max)** , **varbinary(max)** , **nvarchar(max)** , **text**, **ntextxml**e **image** es complejo. Basta con agregar solamente el tamaño medio de los valores de LOB que se esperan y agregarlo al tamaño total del montón.  
  
-   Compresión  
  
     No se puede calcular previamente el tamaño de un montón comprimido.  
  
-   Columnas dispersas  
  
     Para obtener información sobre los requisitos de espacio de las columnas dispersas, vea [Use Sparse Columns](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="see-also"></a>Consulte también  
 [Montones &#40;tablas sin índices agrupados&#41;](../../relational-databases/indexes/heaps-tables-without-clustered-indexes.md)   
 [Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)   
 [Crear índices clúster](../../relational-databases/indexes/create-clustered-indexes.md)   
 [Crear índices no clúster](../../relational-databases/indexes/create-nonclustered-indexes.md)   
 [Calcular el tamaño de una tabla](../../relational-databases/databases/estimate-the-size-of-a-table.md)   
 [Estimar el tamaño de un índice clúster](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [Estimar el tamaño de un índice no clúster](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)   
 [Estimar el tamaño de una base de datos](../../relational-databases/databases/estimate-the-size-of-a-database.md)  
  
  
