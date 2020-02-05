---
title: Desarrollar tipos específicos de componentes de flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 348e219a-b8ff-425e-b9c6-811880101c54
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4d56ea995caa6c363432169c660c5cb9f07d082d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297270"
---
# <a name="developing-specific-types-of-data-flow-components"></a>Desarrollar tipos específicos de componentes de flujo de datos

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="see-also"></a>Consulte también  
 [Comparar soluciones de scripting y objetos personalizados](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [Desarrollar tipos específicos de los componentes de script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
