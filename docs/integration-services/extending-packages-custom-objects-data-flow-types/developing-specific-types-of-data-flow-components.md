---
title: "Desarrollar tipos específicos de componentes de flujo de datos | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects-data-flow-types
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 31c2dafb94bc5f3755d607a3686637b6f8baa205
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="developing-specific-types-of-data-flow-components"></a>Desarrollar tipos específicos de componentes de flujo de datos
  En esta sección se tratan las características específicas del desarrollo de componentes de origen, componentes de transformación con salidas sincrónicas, componentes de transformación con salidas asincrónicas y componentes de destino.  
  
 Para obtener información sobre el desarrollo de componentes en general, vea [Desarrollar un componente de flujo de datos personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Desarrollar un componente de origen personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 Contiene información sobre el desarrollo de un componente que tiene acceso a datos de un origen de datos externo y los proporciona a componentes de nivel inferior en el flujo de datos.  
  
 [Desarrollar un componente de transformación personalizado con salidas sincrónicas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 Contiene información sobre el desarrollo de un componente de transformación cuyas salidas son sincrónicas a sus entradas. Estos componentes no agregan datos al flujo de datos, sino que los procesan a medida que se pasa por ellos.  
  
 [Desarrollar un componente de transformación personalizado con salidas asincrónicas](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 Contiene información sobre el desarrollo de un componente de transformación cuyas salidas no son sincrónicas a sus entradas. Estos componentes reciben datos de componentes de nivel superior, pero también agregan datos al flujo de datos.  
  
 [Desarrollar un componente de destino personalizado](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 Contiene información sobre el desarrollo de un componente que recibe filas de componentes de nivel superior en el flujo de datos y los escribe en un origen de datos externo.  
  
## <a name="reference"></a>Referencia  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 Contiene las clases e interfaces que se utilizan para crear componentes de flujo de datos personalizados.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 Contiene las clases e interfaces no administradas de la tarea de flujo de datos. El desarrollador de software utiliza éstas y el espacio de nombres <xref:Microsoft.SqlServer.Dts.Pipeline> administrado al generar un flujo de datos mediante programación o crear componentes de flujo de datos personalizados.  
  
## <a name="see-also"></a>Ver también  
 [Comparar soluciones de scripting y objetos personalizados](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [Desarrollar tipos específicos de los componentes de script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
