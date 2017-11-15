---
title: Condiciones de reglas de negocios (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d2e0a8c3-4c2e-407c-856e-68d95ebda9ed
caps.latest.revision: "10"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d835567ff20a82b7711206d7d7ce48ef5d5430d7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="business-rule-conditions-master-data-services"></a>Condiciones de reglas de negocios (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], las condiciones de regla de negocios determinan las condiciones que deben cumplirse para que se realicen una o varias acciones.  
  
> [!NOTE]  
>  Las condiciones son opcionales. Si no especifica ninguna condición, se realizarán las acciones siempre que se validen datos con las reglas de negocios.  
  
## <a name="business-rule-conditions"></a>Condiciones de reglas de negocios  
  
|Nombre de condición|Description|  
|--------------------|-----------------|  
|**es igual que**|El atributo seleccionado **es igual que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número, fecha y vínculo.|  
|**no es igual que**|El atributo seleccionado **no es igual que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número, fecha y vínculo.|  
|**es mayor que**|El atributo seleccionado **es mayor que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número y fecha.|  
|**es mayor o igual que**|El atributo seleccionado **es mayor o igual que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número y fecha.|  
|**es menor que**|El atributo seleccionado **es menor que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número y fecha.|  
|**es menor o igual que**|El atributo seleccionado **es menor o igual que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número y fecha.|  
|**empieza por**|El atributo seleccionado **empieza por** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**no empieza por**|El atributo seleccionado **no empieza por** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**termina por**|El atributo seleccionado **termina por** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**no termina por**|El atributo seleccionado **no termina por** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**contiene**|El atributo seleccionado **contiene** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**no contiene**|El atributo seleccionado **no contiene** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**contiene el patrón**|El atributo seleccionado **contiene el patrón** de un atributo determinado, un valor de atributo concreto o está en blanco. Use expresiones regulares de .NET Framework para especificar el patrón.<br /><br /> Para obtener más información sobre las expresiones regulares, consulte [Elementos del lenguaje de expresiones regulares](http://go.microsoft.com/fwlink/?LinkId=164401) en MSDN Library.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**no contiene el patrón**|El atributo seleccionado **no contiene el patrón** de un atributo determinado, un valor de atributo concreto o está en blanco. Use expresiones regulares de .NET Framework para especificar el patrón.<br /><br /> Para obtener más información sobre las expresiones regulares, consulte [Elementos del lenguaje de expresiones regulares](http://go.microsoft.com/fwlink/?LinkId=164401) en MSDN Library.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**contiene el subconjunto**|El atributo seleccionado **contiene el subconjunto** de un atributo seleccionado o de un valor de atributo determinado. Debe especificar la posición inicial para la búsqueda (por ejemplo, 1 indica que se inicie la búsqueda en el primer carácter).<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**no contiene el subconjunto**|El atributo seleccionado **no contiene el subconjunto** de un atributo seleccionado o de un valor de atributo determinado. Debe especificar la posición inicial para la búsqueda (por ejemplo, 1 indica que se inicie la búsqueda en el primer carácter).<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**ha cambiado**|El atributo seleccionado **ha cambiado** desde la última vez que se aplicaron reglas de negocios al miembro. Debe especificar el grupo de cambios del que el atributo es miembro.<br /><br /> Para más información sobre los grupos de seguimiento de cambios, vea [Agregar atributos a un grupo de seguimiento de cambios &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).<br /><br /> Esta condición es válida para los valores de texto, número, fecha y vínculo.|  
|**no ha cambiado**|El atributo seleccionado **no ha cambiado** desde la última vez que se aplicaron reglas de negocios al miembro. Debe especificar el grupo de cambios del que el atributo es miembro.<br /><br /> Para más información sobre los grupos de seguimiento de cambios, vea [Agregar atributos a un grupo de seguimiento de cambios &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).<br /><br /> Esta condición es válida para los valores de texto, número, fecha y vínculo.|  
|**está comprendido entre**|El atributo seleccionado **está comprendido entre** dos valores de atributo determinados.<br /><br /> Esta condición es válida para los valores de texto, número y fecha.|  
|**no está comprendido entre**|El atributo seleccionado **no está comprendido entre** dos valores de atributo determinados.<br /><br /> Esta condición es válida para los valores de texto, número y fecha.|  
  
> [!NOTE]  
>  Cuando una regla de negocios contiene una condición que compara dos valores y la regla se aplica un miembro para el que los dos valores son NULL, ese miembro no pasará la validación.  
  
## <a name="see-also"></a>Vea también  
 [Acciones de reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rule-actions-master-data-services.md)   
 [Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Crear y publicar una regla de negocios &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
