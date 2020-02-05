---
title: Transformación Combinación de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.mergejointrans.f1
- sql13.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- datasets [Integration Services]
- Merge Join transformation
- datasets [Integration Services], joining
- joining datasets [Integration Services]
- joins [SQL Server], SSIS
ms.assetid: cd8b0412-f83b-4bd2-b227-e53dcfd941a8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f963a3f8bf82ed3de76e31b6872ac6475d6dfd83
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297848"
---
# <a name="merge-join-transformation"></a>Combinación de mezcla, transformación

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La transformación Combinación de mezcla proporciona una salida que se genera combinando dos conjuntos de datos ordenados mediante una combinación FULL, LEFT o INNER. Por ejemplo, puede utilizar una combinación LEFT para combinar una tabla que incluye información de productos con una tabla que incluye el país o la región en que se fabricó un producto. El resultado es una tabla que muestra todos los productos y su país o región de origen.  
  
 Puede configurar la transformación Combinación de mezcla de las siguientes maneras:  
  
-   Especificar que la combinación es una combinación FULL, LEFT o INNER.  
  
-   Especificar las columnas utilizadas por la combinación.  
  
-   Especificar si la transformación controla valores NULL como iguales a otros valores NULL.  
  
    > [!NOTE]  
    >  Si los valores NULL no se tratan como valores iguales, la transformación controla los valores NULL de la misma manera que lo hace el Motor de bases de datos de SQL Server.  
  
 Esta transformación tiene dos entradas y una salida. No admite una salida de error.  
  
## <a name="input-requirements"></a>Requisitos de entrada  
 La transformación Combinación de mezcla requiere datos ordenados para sus entradas. Para obtener más información sobre este importante requisito, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
## <a name="join-requirements"></a>Requisitos de combinación  
 La transformación Combinación de mezcla requiere que las columnas combinadas tengan metadatos coincidentes. Por ejemplo, no puede combinar una columna que tenga un tipo de datos numérico con una columna que tenga un tipo de datos de carácter. Si los datos tienen un tipo de datos de cadena, la longitud de la columna de la segunda entrada debe ser menor o igual que la longitud de la columna de la primera entrada con la que se va a combinar.  
  
## <a name="buffer-throttling"></a>Limitación del búfer  
 Ya no tiene que configurar el valor de la propiedad **MaxBuffersPerInput** porque Microsoft ha realizado modificaciones que reducen el riesgo de que la transformación Combinación de mezcla utilice demasiada memoria. Este problema se producía a veces cuando varias entradas de la Combinación de mezcla generaban datos a velocidades desiguales.  
  
## <a name="related-tasks"></a>Related Tasks  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información sobre cómo establecer las propiedades de esta transformación, haga clic en uno de los temas siguientes:  
  
-   [Ampliación de un conjunto de datos con la transformación Combinación de mezcla](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordenación de datos para las transformaciones Mezclar y Combinación de mezcla](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-join-transformation-editor"></a>Editor de transformación Combinación de mezcla
  Use el cuadro de diálogo **Editor de transformación Combinación de mezcla** para especificar el tipo de combinación, las columnas de combinación y las columnas de salida para mezclar dos entradas fusionadas por combinación.  
  
> [!IMPORTANT]  
>  La transformación Combinación de mezcla requiere datos ordenados para sus entradas. Para obtener más información sobre este importante requisito, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### <a name="options"></a>Opciones  
 **Tipo de combinación**  
 Especifique si desea utilizar una combinación interna (inner join), una combinación externa izquierda (left outer join) o una combinación completa (full join).  
  
 **Intercambiar entradas**  
 Para cambiar el orden de las entradas, use el botón **Intercambiar entradas** . Esta selección resulta útil con la opción de combinación externa izquierda (left outer join).  
  
 **Entrada**  
 Seleccione las columnas que desee en la salida combinada de la lista de entradas disponibles.  
  
 Las entradas se muestran en dos tablas independientes. Seleccione las columnas que desea incluir en la salida. Arrastre las columnas para crear una combinación entre las tablas. Para eliminar una combinación, selecciónela y presione la tecla Supr.  
  
 **Columna de entrada**  
 Seleccione una columna de la lista de columnas disponibles para incluirla en la salida combinada de la entrada seleccionada.  
  
 **Alias de salida**  
 Escriba un alias para cada columna de salida. El nombre predeterminado es el de la columna de entrada, pero puede elegir cualquier nombre descriptivo único.  
  
## <a name="see-also"></a>Consulte también  
 [Transformación Mezclar](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Transformación Unión de todo](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
