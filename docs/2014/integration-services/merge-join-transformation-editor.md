---
title: Editor de transformación combinación de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- Merge Join Transformation Editor
ms.assetid: ac06f419-30b3-42aa-8b34-42000bec4285
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 222e21e83ef0b722ea33c45ff5413dd77b88fe12
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84951085"
---
# <a name="merge-join-transformation-editor"></a>Editor de transformación Combinación de mezcla
  Use el cuadro de diálogo **Editor de transformación Combinación de mezcla** para especificar el tipo de combinación, las columnas de combinación y las columnas de salida para mezclar dos entradas fusionadas por combinación.  
  
> [!IMPORTANT]  
>  La transformación Combinación de mezcla requiere datos ordenados para sus entradas. Para obtener más información sobre este importante requisito, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 Para obtener más información acerca de la transformación Combinación de mezcla, vea [Merge Join Transformation](data-flow/transformations/merge-join-transformation.md).  
  
## <a name="options"></a>Opciones  
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
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Ordenar datos para las transformaciones mezclar y combinación de mezcla](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)   
 [Extender un conjunto de objetos mediante la transformación combinación de mezcla](data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)   
 [Transformación mezclar](data-flow/transformations/merge-transformation.md)   
 [Transformación Unión de todo](data-flow/transformations/union-all-transformation.md)  
  
  
