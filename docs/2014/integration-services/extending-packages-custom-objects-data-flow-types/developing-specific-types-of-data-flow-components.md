---
title: Desarrollar tipos específicos de componentes de flujo de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 78810a0599d2345770175bc0ed9bdc06f3195817
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62896337"
---
# <a name="developing-specific-types-of-data-flow-components"></a>Desarrollar tipos específicos de componentes de flujo de datos
  En esta sección se tratan las características específicas del desarrollo de componentes de origen, componentes de transformación con salidas sincrónicas, componentes de transformación con salidas asincrónicas y componentes de destino.  
  
 Para obtener información sobre el desarrollo de componentes en general, vea [Desarrollar un componente de flujo de datos personalizado](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [Desarrollar un componente de origen personalizado](../extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
 Contiene información sobre el desarrollo de un componente que tiene acceso a datos de un origen de datos externo y los proporciona a componentes de nivel inferior en el flujo de datos.  
  
 [Desarrollar un componente de transformación personalizado con salidas sincrónicas](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
 Contiene información sobre el desarrollo de un componente de transformación cuyas salidas son sincrónicas a sus entradas. Estos componentes no agregan datos al flujo de datos, sino que los procesan a medida que se pasa por ellos.  
  
 [Desarrollar un componente de transformación personalizado con salidas asincrónicas](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
 Contiene información sobre el desarrollo de un componente de transformación cuyas salidas no son sincrónicas a sus entradas. Estos componentes reciben datos de componentes de nivel superior, pero también agregan datos al flujo de datos.  
  
 [Desarrollar un componente de destino personalizado](../extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
 Contiene información sobre el desarrollo de un componente que recibe filas de componentes de nivel superior en el flujo de datos y los escribe en un origen de datos externo.  
  
## <a name="reference"></a>Referencia  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 Contiene las clases e interfaces que se utilizan para crear componentes de flujo de datos personalizados.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 Contiene las clases e interfaces no administradas de la tarea de flujo de datos. El desarrollador de software utiliza éstas y el espacio de nombres <xref:Microsoft.SqlServer.Dts.Pipeline> administrado al generar un flujo de datos mediante programación o crear componentes de flujo de datos personalizados.  
  
![Integration Services icono (pequeño)](../media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Consulte también  
 [Comparar soluciones de scripting y objetos personalizados](../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [Desarrollar tipos específicos de los componentes de script](../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)  
  
  
