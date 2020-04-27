---
title: Transformación Combinación de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointrans.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0ef70f4f9d28fc23c0ac0a168447cc1b8867cd27
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62900171"
---
# <a name="merge-join-transformation"></a>Combinación de mezcla, transformación
  La transformación Combinación de mezcla proporciona una salida que se genera combinando dos conjuntos de datos ordenados mediante una combinación FULL, LEFT o INNER. Por ejemplo, puede utilizar una combinación LEFT para combinar una tabla que incluye información de productos con una tabla que incluye el país o la región en que se fabricó un producto. El resultado es una tabla que muestra todos los productos y su país o región de origen.  
  
 Puede configurar la transformación Combinación de mezcla de las siguientes maneras:  
  
-   Especificar que la combinación es una combinación FULL, LEFT o INNER.  
  
-   Especificar las columnas utilizadas por la combinación.  
  
-   Especificar si la transformación controla valores NULL como iguales a otros valores NULL.  
  
    > [!NOTE]  
    >  Si los valores NULL no se tratan como valores iguales, la transformación controla los valores NULL de la misma manera que lo hace el Motor de bases de datos de SQL Server.  
  
 Esta transformación tiene dos entradas y una salida. No admite una salida de error.  
  
## <a name="input-requirements"></a>Requisitos de entrada  
 La transformación Combinación de mezcla requiere datos ordenados para sus entradas. Para obtener más información sobre este importante requisito, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](sort-data-for-the-merge-and-merge-join-transformations.md).  
  
## <a name="join-requirements"></a>Requisitos de combinación  
 La transformación Combinación de mezcla requiere que las columnas combinadas tengan metadatos coincidentes. Por ejemplo, no puede combinar una columna que tenga un tipo de datos numérico con una columna que tenga un tipo de datos de carácter. Si los datos tienen un tipo de datos de cadena, la longitud de la columna de la segunda entrada debe ser menor o igual que la longitud de la columna de la primera entrada con la que se va a combinar.  
  
## <a name="buffer-throttling"></a>Limitación del búfer  
 Ya no tiene que configurar el valor de la propiedad `MaxBuffersPerInput` porque Microsoft ha realizado modificaciones que reducen el riesgo de que la transformación Combinación de mezcla utilice demasiada memoria. Este problema se producía a veces cuando varias entradas de la Combinación de mezcla generaban datos a velocidades desiguales.  
  
## <a name="related-tasks"></a>Related Tasks  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información sobre cómo establecer las propiedades de esta transformación, haga clic en uno de los temas siguientes:  
  
-   [Ampliación de un conjunto de datos con la transformación Combinación de mezcla](merge-join-transformation.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordenación de datos para las transformaciones Mezclar y Combinación de mezcla](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="see-also"></a>Consulte también  
 [Editor de transformación combinación de mezcla](../../merge-join-transformation-editor.md)   
 [Transformación mezclar](merge-transformation.md)   
 [Transformación Unión de todo](union-all-transformation.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
  
