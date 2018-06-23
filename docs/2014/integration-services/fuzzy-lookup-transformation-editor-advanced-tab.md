---
title: Editor de transformación Búsqueda aproximada (pestaña Avanzadas) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.advanced.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: 0a2919be-2ea7-4c06-82b8-0ffad5f0dd83
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 65c7acaab54bbbaa18126e9c1d2ac032e96557da
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114297"
---
# <a name="fuzzy-lookup-transformation-editor-advanced-tab"></a>Editor de transformación Búsqueda aproximada (pestaña Avanzadas)
  Utilice la pestaña **Avanzadas** del cuadro de diálogo **Editor de transformación Búsqueda aproximada** para establecer los parámetros de la búsqueda aproximada.  
  
 Para obtener más información acerca de la transformación Búsqueda aproximada, vea [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Número máximo de coincidencias por búsqueda para la salida**  
 Especifique el número máximo de coincidencias que la transformación puede devolver para cada fila de entrada. El valor predeterminado es **1**.  
  
 **Umbral de similitud**  
 Establezca el umbral de similitud en el nivel de componente con el control deslizante. Cuanto más se acerque el valor a 1, más deberá parecerse el valor de búsqueda al valor de origen para que pueda calificarse como coincidencia. Al aumentar el umbral se puede mejorar la velocidad de la coincidencia ya que se tendrán en cuanta menos registros candidatos.  
  
 **Delimitadores de token**  
 Especifique los delimitadores que la transformación utilizará para dividir en tokens los valores de las columnas.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación Búsqueda aproximada &#40;pestaña de la tabla de referencia&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [Editor de transformación Búsqueda aproximada &#40;pestaña columnas&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-columns-tab.md)  
  
  