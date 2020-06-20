---
title: Editor de transformación agrupación aproximada (pestaña administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.connection.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 47b1446d-5331-473c-9cb5-a98b1f55bf5f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8b06f9202bc158d1f64a11c9814792c7fe63ee9d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966345"
---
# <a name="fuzzy-grouping-transformation-editor-connection-manager-tab"></a>Editor de transformación Agrupación aproximada (pestaña Administrador de conexiones)
  Use la pestaña **Administrador de conexiones** del cuadro de diálogo **Editor de transformación Agrupación aproximada** para seleccionar una conexión existente o crear una nueva.  
  
> [!NOTE]  
>  El servidor especificado por la conexión debe ejecutar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La transformación Agrupación aproximada crea objetos de datos temporales en tempdb que pueden ser tan grandes como toda la entrada de la transformación. Mientras se ejecuta la transformación, se emiten consultas de servidor a esos objetos temporales. Esto puede afectar al rendimiento general del servidor.  
  
 Para obtener más información acerca de la transformación Agrupación aproximada, vea [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Administrador de conexiones de OLE DB**  
 Seleccione un administrador de conexiones OLE DB existente con el cuadro de lista, o bien cree una conexión con el botón **Nuevo** .  
  
 **Nuevo**  
 Cree una conexión mediante el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Identificar filas de datos similares mediante la transformación Agrupación aproximada](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
