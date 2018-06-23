---
title: Validación (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 98eb49e7-b190-4a21-8316-08c07cde14ed
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 769e3e1cba3179ab9a3040094f1d88f79c3c6d55
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201398"
---
# <a name="validation-master-data-services"></a>Validación (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], los datos se validan para asegurarse de su precisión. Cierta validación se realiza automáticamente, mientras que otra se basa en las reglas de negocios creadas por los administradores.  
  
## <a name="when-data-validation-occurs"></a>Cuándo se produce la validación de datos  
 La validación se produce en momentos diferentes y se muestra de forma distinta en la aplicación web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
|Tipo de validación|Estándares determinados por|Cuándo se produce|Se muestra en la interfaz de usuario web de Master Data Manager como|Se muestra en el complemento de Excel como|¿Se guardan los datos en el repositorio MDS?|  
|---------------------|-----------------------------|--------------------|---------------------------------------------------|-------------------------------------------|------------------------------------------|  
|Validación de la regla de negocios|Un administrador de MDS|Automáticamente cuando un usuario agrega o edita datos.<br /><br /> Manualmente cuando un usuario aplica reglas de negocios.<br /><br /> Manualmente cuando un administrador en el área funcional **Administración de versiones** de la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] valida una versión comparándola con las reglas de negocios.|Errores de validación|ValidationStatus|Sí|  
|Validación del tipo de datos y el contenido|Un administrador de MDS, al crear objetos de modelo (por ejemplo, la longitud o el tipo de datos de un atributo)|Automáticamente cuando un usuario agrega o edita datos|Errores de entrada|InputStatus|no|  
|Validación del tipo de datos y el contenido|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o bien [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|Automáticamente cuando un usuario agrega o edita datos|Errores de entrada|InputStatus|no|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear reglas de negocios y publicarlas para validar los datos con ellas.|[Crear y publicar una regla de negocios &#40;Master Data Services&#41;](create-and-publish-a-business-rule-master-data-services.md)|  
|Validar una versión de datos según las reglas de negocios. Solo los administradores.|[Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)|  
|Validar subconjuntos específicos de datos según las reglas de negocios. Todos los usuarios con permiso en el área funcional **Explorador** .|[Validar miembros específicos con las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|Validar subconjuntos específicos de datos según las reglas de negocios. Todos los usuarios con permiso en el área funcional **Explorador** que usen [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].|[Aplicar reglas de negocios &#40;complemento MDS para Excel&#41;](microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)|  
  
## <a name="see-also"></a>Vea también  
 [Las reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
  