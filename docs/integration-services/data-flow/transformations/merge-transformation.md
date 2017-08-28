---
title: "Transformación mezclar | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.mergetrans.f1
- sql13.dts.designer.mergetransformation.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- merging data [Integration Services]
- Merge transformation
- combining datasets
- datasets [Integration Services], merging
ms.assetid: cff8690c-07ac-46a0-aab5-20bd4848c677
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: 4c3eead08bb91d43f83782682a122da278ac051f
ms.contentlocale: es-es
ms.lasthandoff: 08/19/2017

---
# <a name="merge-transformation"></a>Mezclar, transformación
  La transformación Mezclar combina dos conjuntos de datos ordenados en un solo conjunto de datos. Las filas de cada conjunto de datos se insertan en la salida en función de los valores de sus columnas de clave.  
  
 Si incluye la transformación Mezclar en un flujo de datos, podrá realizar las siguientes tareas:  
  
-   Combinar datos de dos orígenes de datos, como tablas y archivos.  
  
-   Crear conjuntos de datos complejos anidando transformaciones de combinación.  
  
-   Volver a combinar filas después de corregir errores en los datos.  
  
 La transformación Mezclar es similar a las transformaciones Unión de todo. Use la transformación Unión de todo en lugar de la transformación Mezclar en las siguientes situaciones:  
  
-   Las entradas de la transformación no están ordenadas.  
  
-   La salida combinada no tiene que ordenarse.  
  
-   La transformación tiene más de dos entradas.  
  
## <a name="input-requirements"></a>Requisitos de entrada  
 La transformación Mezclar requiere datos ordenados para sus entradas. Para obtener más información sobre este importante requisito, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 La transformación Mezclar también requiere que las columnas combinadas en sus entradas tengan metadatos coincidentes. Por ejemplo, no puede combinar una columna que tenga un tipo de datos numérico con una columna que tenga un tipo de datos de carácter. Si los datos tienen un tipo de datos de cadena, la longitud de la columna de la segunda entrada debe ser menor o igual que la longitud de la columna de la primera entrada con la que se va a combinar.  
  
 En el Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , la interfaz de usuario para la transformación Mezclar asigna automáticamente las columnas que tienen los mismos metadatos. Después puede asignar manualmente otras columnas con tipos de datos compatibles.  
  
 Esta transformación tiene dos entradas y una salida. No admite una salida de error.  
  
## <a name="configuration-of-the-merge-transformation"></a>Configuración de la transformación Mezclar  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 Para obtener información detallada acerca de cómo establecer propiedades, vea los temas siguientes:  
  
-   [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordenar datos para la combinación y transformaciones de combinación de mezcla](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="merge-transformation-editor"></a>Editor de transformación Mezclar
  Use el **Editor de transformación Mezclar** para especificar las columnas de dos conjuntos de datos ordenados que desee combinar.  
  
> [!IMPORTANT]  
>  La transformación Mezclar requiere datos ordenados para sus entradas. Para más información sobre este importante requisito, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
### <a name="options"></a>Opciones  
 **Nombre de la columna de salida**  
 Especifique el nombre de la columna de salida.  
  
 **Entrada de Mezclar 1**  
 Seleccione la columna que desea mezclar como Entrada de Mezclar 1.  
  
 **Entrada de Mezclar 2**  
 Seleccione la columna que desea mezclar como Entrada de Mezclar 2.  
  
## <a name="see-also"></a>Vea también  
 [Transformación Combinación de mezcla](../../../integration-services/data-flow/transformations/merge-join-transformation.md)   
 [Unión transformación todo](../../../integration-services/data-flow/transformations/union-all-transformation.md)   
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
