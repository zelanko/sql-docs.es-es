---
title: Editor de transformación búsqueda (página avanzadas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.advanced.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: f3395c65-0320-47f9-8d83-daaa082d8713
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 02aa291ef4d282fa77c21f93cc0700cbe1a3032c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440282"
---
# <a name="lookup-transformation-editor-advanced-page"></a>Editor de transformación Búsqueda (página Avanzadas)
  Utilice la página **Avanzadas** del cuadro de diálogo **Editor de transformación Búsqueda** para configurar el almacenamiento parcial en caché y modificar la instrucción SQL para la transformación Búsqueda.  
  
 Para obtener más información acerca de la transformación Búsqueda, vea [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
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
>  La instrucción SQL opcional que se especifica en esta página invalida y reemplaza el nombre de tabla que se especificó en la página **Conexión** del **Editor de transformación Búsqueda**. Para más información, vea [Editor de transformación Búsqueda &#40;página Conexión&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md).  
  
 **Establecer parámetros**  
 Asigne columnas de entrada a parámetros mediante el cuadro de diálogo **Establecer parámetros de consulta** .  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada del blog, [Lookup cache modes](https://go.microsoft.com/fwlink/?LinkId=219518) en blogs.msdn.com  
  
## <a name="see-also"></a>Consulte también  
 [Editor de transformación búsqueda &#40;página general&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de transformación búsqueda &#40;página de conexión&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [Editor de transformación búsqueda &#40;página columnas&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [Editor de transformación búsqueda &#40;página salida de error&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Búsqueda aproximada, transformación](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
