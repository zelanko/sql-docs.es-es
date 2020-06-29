---
title: Editor de transformación extracción de términos (pestaña exclusión) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextraction.inclusionexclusion.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 90110d95-fd97-4542-9cda-832c86606130
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e4597f3100e7c867b888d8af1d05204e2c271208
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440042"
---
# <a name="term-extraction-transformation-editor-exclusion-tab"></a>Editor de transformación Extracción de términos (pestaña Exclusión)
  Use la pestaña **Exclusión** del cuadro de diálogo **Editor de transformación Extracción de términos** para establecer una conexión con una tabla de exclusión y especificar las columnas que contienen términos de exclusión.  
  
 Para obtener más información acerca de la transformación Extracción de términos, vea [Term Extraction Transformation](data-flow/transformations/term-extraction-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Utilizar términos de exclusión**  
 Esta opción indica si se excluirán términos específicos durante la extracción de términos mediante la especificación de una columna que contiene los términos de exclusión. Si desea excluir términos, debe especificar las siguientes propiedades del origen:  
  
 **Administrador de conexiones de OLE DB**  
 Permite seleccionar un administrador de conexiones OLE DB o crear una conexión haciendo clic en **Nueva**.  
  
 **Nuevo**  
 Crea una conexión a una base de datos mediante el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
 **Tabla o vista**  
 Permite seleccionar la tabla o vista que contiene los términos de exclusión.  
  
 **Columna**  
 Permite seleccionar la columna de la tabla o vista que contiene los términos de exclusión.  
  
 **Configurar la salida de errores**  
 Use el cuadro de diálogo [Configurar la salida de errores](../../2014/integration-services/configure-error-output.md) para especificar las opciones de control de errores para las filas que provocan errores.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformación extracción de términos &#40;pestaña extracción de términos&#41;](../../2014/integration-services/term-extraction-transformation-editor-term-extraction-tab.md)   
 [Editor de transformación extracción de términos &#40;pestaña avanzadas&#41;](../../2014/integration-services/term-extraction-transformation-editor-advanced-tab.md)   
 [Búsqueda de términos, transformación](data-flow/transformations/lookup-transformation.md)  
  
  
