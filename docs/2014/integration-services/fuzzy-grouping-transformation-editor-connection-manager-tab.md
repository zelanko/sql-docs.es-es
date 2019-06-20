---
title: Editor de transformación Agrupación aproximada (pestaña Administrador de conexiones) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7cfee2c2a79410d73eb6ca4da47f0fd361a24fb2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058339"
---
# <a name="fuzzy-grouping-transformation-editor-connection-manager-tab"></a>Editor de transformación Agrupación aproximada (pestaña Administrador de conexiones)
  Use la pestaña **Administrador de conexiones** del cuadro de diálogo **Editor de transformación Agrupación aproximada** para seleccionar una conexión existente o crear una nueva.  
  
> [!NOTE]  
>  El servidor especificado por la conexión debe ejecutar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La transformación Agrupación aproximada crea objetos de datos temporales en tempdb que pueden ser tan grandes como toda la entrada de la transformación. Mientras se ejecuta la transformación, se emiten consultas de servidor a esos objetos temporales. Esto puede afectar al rendimiento general del servidor.  
  
 Para obtener más información acerca de la transformación Agrupación aproximada, vea [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Administrador de conexiones OLE DB**  
 Seleccione un administrador de conexiones OLE DB existente con el cuadro de lista, o bien cree una conexión con el botón **Nuevo** .  
  
 **Nueva**  
 Permite crear una conexión con el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** .  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Identificar filas de datos similares mediante la transformación Agrupación aproximada](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
