---
title: Preparar datos para su presentación en una región de datos Tablix (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: fbb00dc6-7887-480c-b771-cab6fecb8dcc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86418fd892c4f403f1e0207073a28e7933eb4b58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105417"
---
# <a name="preparing-data-for-display-in-a-tablix-data-region-report-builder-and-ssrs"></a>Preparar datos para su presentación en una región de datos Tablix (Generador de informes y SSRS)
  Una región de datos Tablix muestra los datos de un conjunto de datos. Puede ver todos los datos recuperados para el conjunto de datos o puede crear filtros para ver solo un subconjunto de los datos. También puede agregar expresiones condicionales para rellenar los valores NULL o modificar la consulta para que un conjunto de datos incluya columnas que definan el criterio de ordenación para una columna existente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="working-with-nulls-and-blanks-in-field-values"></a>Trabajar con valores de campo NULL y vacíos  
 Los datos para la colección de campos de un conjunto de datos incluyen todos los valores recuperados del origen de datos en tiempo de ejecución, incluyendo los valores NULL y los valores en blanco. Normalmente, no es posible distinguir los valores NULL y los valores en blanco. En la mayoría de los casos, éste es el comportamiento deseado. Por ejemplo, las funciones de agregado numéricas como [Sum](report-builder-functions-sum-function.md) y [Avg](report-builder-functions-avg-function.md) omiten los valores NULL. Para más información, vea [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
 Si desea tratar de manera diferente los valores NULL, puede usar expresiones condicionales o código personalizado para sustituir el valor NULL por un valor personalizado. Por ejemplo, la expresión siguiente sustituye el valor del campo por el texto `Null` siempre que el campo `[Size]`contenga un valor NULL.  
  
```  
=IIF(Fields!Size.Value IS NOTHING,"Null",Fields!Size.Value)  
```  
  
 Para obtener más información sobre cómo eliminar los valores NULL en los datos antes de recuperar estos de un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)] , vea "Valores NULL" y "Combinaciones y valores NULL" en la documentación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en los [Libros en pantalla de SQL Server](https://go.microsoft.com/fwlink/?linkid=120955).  
  
## <a name="handling-null-field-names"></a>Controlar nombres de campo nulos  
 Comprobar la existencia de valores NULL en una expresión es apropiado siempre que el campo exista en el conjunto de resultados de la consulta. Usando código personalizado, puede comprobar si el propio campo se encuentra presente en los campos devueltos desde el origen de datos en tiempo de ejecución. Para obtener más información, vea [Referencias a la colección de campos de conjunto de datos &#40;Generador de informes y SSRS&#41;](built-in-collections-dataset-fields-collection-references-report-builder.md).  
  
## <a name="adding-a-sort-order-column"></a>Agregar una columna de criterio de ordenación  
 De forma predeterminada, es posible ordenar alfabéticamente los valores de un campo de conjunto de datos. Para ordenar por un criterio de ordenación diferente, puede agregar una nueva columna al conjunto de datos que defina el criterio de ordenación que desea en una región de datos. Por ejemplo, para ordenar por el campo `[Color]` y colocar primero los elementos blancos y negros, puede agregar la columna `[ColorSortOrder]`que se muestra en la consulta siguiente:  
  
```  
SELECT ProductID, p.Name, Color,  
   CASE  
      WHEN p.Color = 'White' THEN 1  
      WHEN p.Color = 'Black' THEN 2  
      WHEN p.Color = 'Blue' THEN 3  
      WHEN p.Color = 'Yellow' THEN 4  
      ELSE 5  
   END As ColorSortOrder  
FROM Production.Product p  
```  
  
 Para ordenar una región de datos de tabla según este criterio de ordenación, establezca la expresión de ordenación en el grupo de detalles en `=Fields!ColorSortOrder.Value`. Para más información, vea [Ordenar datos en una región de datos &#40;Generador de informes y SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](../report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
