---
title: "Editor de transformación combinación de mezcla | Documentos de Microsoft"
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
- sql13.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- Merge Join Transformation Editor
ms.assetid: ac06f419-30b3-42aa-8b34-42000bec4285
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6bba110363b36294a67880f3efbdec52e1c6db0d
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="merge-join-transformation-editor"></a>Editor de transformación Combinación de mezcla
  Use el cuadro de diálogo **Editor de transformación Combinación de mezcla** para especificar el tipo de combinación, las columnas de combinación y las columnas de salida para mezclar dos entradas fusionadas por combinación.  
  
> [!IMPORTANT]  
>  La transformación Combinación de mezcla requiere datos ordenados para sus entradas. Para más información sobre este importante requisito, vea [Ordenar datos para las transformaciones Mezclar y Combinación de mezcla](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 Para obtener más información acerca de la transformación Combinación de mezcla, vea [Merge Join Transformation](../../../integration-services/data-flow/transformations/merge-join-transformation.md).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Ordenar datos para la combinación y transformaciones de combinación de mezcla](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)   
 [Ampliar un conjunto de datos mediante la transformación combinación de mezcla](../../../integration-services/data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)   
 [Transformación mezclar](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Unión transformación todo](../../../integration-services/data-flow/transformations/union-all-transformation.md)  
  
  
