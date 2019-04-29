---
title: Condiciones de reglas de negocios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d2e0a8c3-4c2e-407c-856e-68d95ebda9ed
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d5089921156f97509e157f771dbe20e1c33cf569
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925973"
---
# <a name="business-rule-conditions-master-data-services"></a>Condiciones de reglas de negocios (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], las condiciones de regla de negocios determinan las condiciones que deben cumplirse para que se realicen una o varias acciones.  
  
> [!NOTE]  
>  Las condiciones son opcionales. Si no especifica ninguna condición, se realizarán las acciones siempre que se validen datos con las reglas de negocios.  
  
## <a name="business-rule-conditions"></a>Condiciones de reglas de negocios  
  
|Nombre de condición|Descripción|  
|--------------------|-----------------|  
|**es igual que**|El atributo seleccionado **es igual que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número, fecha y vínculo.|  
|**no es igual que**|El atributo seleccionado **no es igual que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número, fecha y vínculo.|  
|**es mayor que**|El atributo seleccionado **es mayor que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número y fecha.|  
|**es mayor o igual que**|El atributo seleccionado **es mayor o igual que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número y fecha.|  
|**es menor que**|El atributo seleccionado **es menor que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número y fecha.|  
|**es menor o igual que**|El atributo seleccionado **es menor o igual que** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto, número y fecha.|  
|**empieza por**|El atributo seleccionado **empieza por** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**termina por**|El atributo seleccionado **termina por** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**contiene**|El atributo seleccionado **contiene** un atributo determinado, un valor de atributo concreto o está en blanco.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**contiene el patrón**|El atributo seleccionado **contiene el patrón** de un atributo determinado, un valor de atributo concreto o está en blanco. Use expresiones regulares de .NET Framework para especificar el patrón.<br /><br /> Para obtener más información sobre las expresiones regulares, consulte [Elementos del lenguaje de expresiones regulares](https://go.microsoft.com/fwlink/?LinkId=164401) en MSDN Library.<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**contiene el subconjunto**|El atributo seleccionado **contiene el subconjunto** de un atributo seleccionado o de un valor de atributo determinado. Debe especificar la posición inicial para la búsqueda (por ejemplo, 1 indica que se inicie la búsqueda en el primer carácter).<br /><br /> Esta condición es válida para los valores de texto y vínculo.|  
|**ha cambiado**|El atributo seleccionado **ha cambiado** desde la última vez que se aplicaron reglas de negocios al miembro. Debe especificar el grupo de cambios del que el atributo es miembro.<br /><br /> Para más información sobre los grupos de seguimiento de cambios, vea [Agregar atributos a un grupo de seguimiento de cambios &#40;Master Data Services&#41;](add-attributes-to-a-change-tracking-group-master-data-services.md).<br /><br /> Esta condición es válida para los valores de texto, número, fecha y vínculo.|  
|**está comprendido entre**|El atributo seleccionado **está comprendido entre** dos valores de atributo determinados.<br /><br /> Esta condición es válida para los valores de texto, número y fecha.|  
  
> [!NOTE]  
>  Cuando una regla de negocios contiene una condición que compara dos valores y la regla se aplica un miembro para el que los dos valores son NULL, ese miembro no pasará la validación.  
  
## <a name="see-also"></a>Vea también  
 [Acciones de reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/business-rule-actions-master-data-services.md)   
 [Reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)   
 [Crear y publicar una regla de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
