---
title: Editor de transformación extracción de términos (pestaña exclusión) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextraction.inclusionexclusion.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 90110d95-fd97-4542-9cda-832c86606130
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c6292fa7798c9f9d76868b4230317eb99a1f8b3d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766288"
---
# <a name="term-extraction-transformation-editor-exclusion-tab"></a>Editor de transformación Extracción de términos (pestaña Exclusión)
  Use la pestaña **Exclusión** del cuadro de diálogo **Editor de transformación Extracción de términos** para establecer una conexión con una tabla de exclusión y especificar las columnas que contienen términos de exclusión.  
  
 Para obtener más información acerca de la transformación Extracción de términos, vea [Term Extraction Transformation](data-flow/transformations/term-extraction-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Utilizar términos de exclusión**  
 Esta opción indica si se excluirán términos específicos durante la extracción de términos mediante la especificación de una columna que contiene los términos de exclusión. Si desea excluir términos, debe especificar las siguientes propiedades del origen:  
  
 **Administrador de conexiones OLE DB**  
 Permite seleccionar un administrador de conexiones OLE DB o crear una conexión haciendo clic en **Nueva**.  
  
 **Nueva**  
 Crea una conexión a una base de datos mediante el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
 **Tabla o vista**  
 Permite seleccionar la tabla o vista que contiene los términos de exclusión.  
  
 **Columna**  
 Permite seleccionar la columna de la tabla o vista que contiene los términos de exclusión.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](../../2014/integration-services/configure-error-output.md) para especificar las opciones de control de errores para las filas que provocan errores.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación Extracción de términos &#40;pestaña Extracción de términos&#41;](../../2014/integration-services/term-extraction-transformation-editor-term-extraction-tab.md)   
 [Editor de transformación Extracción de términos &#40;pestaña Avanzadas&#41;](../../2014/integration-services/term-extraction-transformation-editor-advanced-tab.md)   
 [Transformación Búsqueda de términos](data-flow/transformations/lookup-transformation.md)  
  
  
