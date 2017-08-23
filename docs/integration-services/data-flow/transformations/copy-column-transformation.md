---
title: "Transformación Copiar columna | Documentos de Microsoft"
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
- sql13.dts.designer.copycolumntrans.f1
helpviewer_keywords:
- columns [Integration Services], copying
- copying columns
- Copy Column transformation
ms.assetid: 1c72a313-9026-46bc-a57f-c6b3f47346f8
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3039b400b136b62840c40b463bb1d8f53a43251d
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="copy-column-transformation"></a>Copiar columna, transformación
  La transformación Copiar columna crea columnas nuevas copiando columnas de entrada y agregando las columnas nuevas a la salida de transformación. En una fase posterior del flujo de datos se pueden aplicar distintas transformaciones a las copias de columnas. Por ejemplo, puede usar la transformación Copiar columna para crear una copia de una columna y después convertir los datos copiados a mayúsculas mediante la transformación Mapa de caracteres, o aplicar agregaciones a la nueva columna mediante la transformación Agregado.  
  
## <a name="configuration-of-the-copy-column-transformation"></a>Configuración de la transformación Copiar columna  
 Puede configurar la transformación Copiar columna especificando las columnas de entrada que desea copiar. Puede crear varias copias de una columna o crear copias de varias columnas en una operación.  
  
 Esta transformación tiene una entrada y una salida. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Copiar columna** , vea [Copy Column Transformation Editor](../../../integration-services/data-flow/transformations/copy-column-transformation-editor.md).  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vea también  
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
