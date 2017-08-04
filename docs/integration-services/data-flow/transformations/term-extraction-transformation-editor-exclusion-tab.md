---
title: "Editor de transformación extracción de términos (pestaña exclusión) | Documentos de Microsoft"
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
- sql13.dts.designer.termextraction.inclusionexclusion.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 90110d95-fd97-4542-9cda-832c86606130
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 50d62aa983a1a5f12def175a375740155596fb65
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="term-extraction-transformation-editor-exclusion-tab"></a>Editor de transformación Extracción de términos (pestaña Exclusión)
  Use la pestaña **Exclusión** del cuadro de diálogo **Editor de transformación Extracción de términos** para establecer una conexión con una tabla de exclusión y especificar las columnas que contienen términos de exclusión.  
  
 Para obtener más información acerca de la transformación Extracción de términos, vea [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Utilizar términos de exclusión**  
 Esta opción indica si se excluirán términos específicos durante la extracción de términos mediante la especificación de una columna que contiene los términos de exclusión. Si desea excluir términos, debe especificar las siguientes propiedades del origen:  
  
 **OLE DB, administrador de conexiones**  
 Permite seleccionar un administrador de conexiones OLE DB o crear una conexión haciendo clic en **Nueva**.  
  
 **Nueva**  
 Crea una conexión a una base de datos mediante el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
 **Tabla o vista**  
 Permite seleccionar la tabla o vista que contiene los términos de exclusión.  
  
 **Columna**  
 Permite seleccionar la columna de la tabla o vista que contiene los términos de exclusión.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar las opciones de control de errores para las filas que provocan errores.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación extracción de términos &#40; Término pestaña extracción &#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-term-extraction-tab.md)   
 [Editor de transformación extracción de términos &#40; Ficha Opciones avanzadas &#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-advanced-tab.md)   
 [Transformación Búsqueda de términos](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
  
