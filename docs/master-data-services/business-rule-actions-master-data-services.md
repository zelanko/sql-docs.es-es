---
title: Acciones de reglas de negocios
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cdc4daca-3dff-46d8-b7f0-57f7826dd61a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 3aa704289844143dc07f63a384269a1ff45f31b9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "73729736"
---
# <a name="business-rule-actions-master-data-services"></a>Acciones de reglas de negocios (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], las acciones de regla de negocios son el resultado de las evaluaciones de condiciones de reglas de negocios. Si una condición es TRUE, se inicia la acción.  
  
> [!NOTE]  
>  Para las acciones de valor predeterminado y de cambiar valor, si el valor generado supera la longitud máxima del atributo, el valor generado se trunca.  
  
## <a name="default-value-actions"></a>Acciones de valor predeterminado  
 Las acciones de**valor predeterminado** establecen el valor predeterminado de un atributo especificado. Los usuarios con permiso pueden cambiar estos valores predeterminados.  
  
|Nombre del valor|Descripción|  
|----------------|-----------------|  
|**tiene como valor predeterminado**|El atributo seleccionado **se establece de manera predeterminada** en un atributo específico, un valor de atributo determinado o está vacío.<br /><br /> Esta acción es válida para los valores de texto, número, fecha y vínculo.|  
|**tiene como valor predeterminado un valor generado**|El atributo seleccionado **tiene como valor predeterminado un valor generado** que se determina especificando un valor de inicio y un valor incremental.<br /><br /> Esta acción es válida para los valores de texto y de número.|  
|**tiene como valor predeterminado un valor concatenado**|El atributo seleccionado **tiene como valor predeterminado un valor concatenado** que se determina especificando varios atributos.<br /><br /> Esta acción es válida para los valores de texto y vínculo.|  
  
## <a name="change-value-actions"></a>Acciones de cambiar valor  
 Las acciones de**cambiar valor** actualizan el valor de un atributo o valor especificado. Los usuarios solo pueden cambiar estos valores si el valor nuevo hace que la acción se establezca en TRUE.  
  
|Nombre del valor|Descripción|  
|----------------|-----------------|  
|**Es igual a**|El atributo seleccionado se cambia a un valor de atributo definido, a otro atributo o el valor se queda vacío.<br /><br /> Esta acción es válida para los valores de texto, número, fecha y vínculo.|  
|**es igual a un valor concatenado**|El atributo seleccionado se cambia a un valor concatenado, que se determina especificando varios atributos.<br /><br /> Esta acción es válida para los valores de texto y vínculo.|  
  
## <a name="validation-actions"></a>Acciones de validación  
 Cuando las acciones de**validación** no se evalúan como TRUE, se envía un correo electrónico a un usuario o un grupo especificados. Para confirmar una versión, todas las acciones de validación deben evaluarse como TRUE.  
  
 Las únicas excepciones son las acciones **es obligatorio** y **no es válido** . Estas acciones se deben combinar con una acción para cambiar valores, de forma que los datos se puedan validar correctamente y se pueda confirmar la versión.  
  
|Nombre de la validación|Descripción|  
|---------------------|-----------------|  
|**es obligatorio**|El atributo seleccionado **es obligatorio**, lo cual indica que no puede ser NULL ni estar vacío.<br /><br /> Esta acción es válida para los valores de texto, número, fecha y vínculo.|  
|**no es válido**|El atributo seleccionado **no es válido**.<br /><br /> Esta acción es válida para los valores de texto, número, fecha y vínculo.|  
|**debe contener el patrón**|El atributo seleccionado **debe contener el patrón** que se ha especificado. Use expresiones regulares de .NET Framework para especificar el patrón.<br /><br /> Para obtener más información acerca de las expresiones regulares, vea [elementos del lenguaje de expresiones regulares](https://go.microsoft.com/fwlink/?LinkId=164401) en MSDN Library.<br /><br /> Esta acción es válida para los valores de texto y vínculo.|  
|**debe ser único**|El atributo seleccionado **debe ser único** de forma independiente o en combinación con atributos definidos.<br /><br /> **Procedimiento recomendado** : combine esta acción con una condición obligatoria para asegurarse de la validez de los campos de índice en los sistemas de suscripción.<br /><br /> Esta acción es válida para los valores de texto, número, fecha y vínculo.<br /><br /> **NOTA**: Si el primer atributo es de tipo DateTime, no se puede usar en combinación con un atributo de tipo Numeric o Text. Si el primer atributo es de tipo Numeric, no se puede usar en combinación con un atributo de tipo DateTime.|  
|**debe tener uno de los siguientes valores**|El atributo seleccionado **debe tener uno de los valores** especificados en una lista.<br /><br /> Esta acción es válida para los valores de texto.|  
|**debe ser mayor que**|El atributo seleccionado **debe ser mayor que** un atributo determinado, un valor de atributo concreto o estar en blanco.<br /><br /> Esta acción es válida para los valores de texto, número y fecha.|  
|**debe ser igual que**|El atributo seleccionado **debe ser igual que** un valor de atributo definido, otro atributo o estar en blanco.<br /><br /> Esta acción es válida para los valores de texto, número, fecha y vínculo.|  
|**debe ser mayor o igual que**|El atributo seleccionado **debe ser mayor o igual que** un atributo determinado, un valor de atributo concreto o estar en blanco.<br /><br /> Esta acción es válida para los valores de texto, número y fecha.|  
|**debe ser menor que**|El atributo seleccionado **debe ser menor que** un atributo determinado, un valor de atributo concreto o estar en blanco.<br /><br /> Esta acción es válida para los valores de texto, número y fecha.|  
|**debe ser menor o igual que**|El atributo seleccionado **debe ser menor o igual que** un atributo determinado, un valor de atributo concreto o estar en blanco.<br /><br /> Esta acción es válida para los valores de texto, número y fecha.|  
|**debe estar comprendido entre**|El atributo seleccionado **debe estar comprendido entre** dos atributos o valores de atributo determinados.<br /><br /> Esta acción es válida para los valores de texto, número y fecha.|  
|**debe tener una longitud mínima de**|El atributo seleccionado **debe tener una longitud mínima** del valor especificado.<br /><br /> Esta acción es válida para los valores de texto y vínculo.|  
|**debe tener una longitud máxima de**|El atributo seleccionado **debe tener una longitud máxima** del valor especificado.<br /><br /> Esta acción es válida para los valores de texto y vínculo.|  
  
## <a name="external-action"></a>Acción externa  
 Las acciones de tipo**Externa** interactúan con aplicaciones fuera de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
|Nombre de la acción|Descripción|  
|-----------------|-----------------|  
|**iniciar flujo de trabajo**|Inicia un flujo de trabajo externo. Los datos que provocaron esta acción se pasan al flujo de trabajo. Para obtener más información, vea el artículo sobre [Integración del flujo de trabajo de SharePoint Master Data Services](https://msdn.microsoft.com/library/gg690195.aspx).<br /><br /> Esta acción es válida para los valores de texto, número, fecha y vínculo.|  
  
## <a name="see-also"></a>Consulte también  
 [Condiciones de reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rule-conditions-master-data-services.md)   
 [Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Crear y publicar una regla de negocios &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
