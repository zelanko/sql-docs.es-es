---
title: "Editor de transformación búsqueda (página avanzadas) | Documentos de Microsoft"
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
- sql13.dts.designer.lookuptransformation.advanced.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: f3395c65-0320-47f9-8d83-daaa082d8713
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 13b342d7db5106451f7355c7dd1672181443f18d
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="lookup-transformation-editor-advanced-page"></a>Editor de transformación Búsqueda (página Avanzadas)
  Utilice la página **Avanzadas** del cuadro de diálogo **Editor de transformación Búsqueda** para configurar el almacenamiento parcial en caché y modificar la instrucción SQL para la transformación Búsqueda.  
  
 Para obtener más información acerca de la transformación Búsqueda, vea [Lookup Transformation](../../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Tamaño de caché (32 bits)**  
 Ajuste el tamaño de caché (en megabytes) para los equipos de 32 bits. El valor predeterminado es 5 megabytes.  
  
 **Tamaño de caché (64 bits)**  
 Ajuste el tamaño de caché (en megabytes) para los equipos de 64 bits. El valor predeterminado es 5 megabytes.  
  
 **Habilitar caché para filas sin entradas coincidentes**  
 Almacene en caché filas sin entradas coincidentes en el conjunto de datos de referencia.  
  
 **Asignación de caché**  
 Especifique el porcentaje de caché que se debe asignar a las filas sin entradas coincidentes en el conjunto de datos de referencia.  
  
 **Modificar la instrucción SQL**  
 Modifique la instrucción SQL que se utiliza para generar el conjunto de datos de referencia.  
  
> [!NOTE]  
>  La instrucción SQL opcional que se especifica en esta página invalida y reemplaza el nombre de tabla que se especificó en la página **Conexión** del **Editor de transformación Búsqueda**. Para más información, vea [Editor de transformación Búsqueda &#40;página Conexión&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md).  
  
 **Establecer parámetros**  
 Asigne columnas de entrada a parámetros mediante el cuadro de diálogo **Establecer parámetros de consulta** .  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada del blog, [Lookup cache modes](http://go.microsoft.com/fwlink/?LinkId=219518) en blogs.msdn.com  
  
## <a name="see-also"></a>Vea también  
 [Editor de transformación Búsqueda &#40; Página general &#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-general-page.md)   
 [Editor de transformación Búsqueda &#40; Página de conexión &#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-connection-page.md)   
 [Editor de transformación Búsqueda &#40; Página columnas &#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-columns-page.md)   
 [Editor de transformación Búsqueda &#40; Página de salida de error &#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md)   
 [Referencia de mensajes y Error de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Transformación Búsqueda aproximada](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
