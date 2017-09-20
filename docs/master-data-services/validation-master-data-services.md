---
title: "Validación (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 98eb49e7-b190-4a21-8316-08c07cde14ed
caps.latest.revision: 12
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 3f536db99b75542de49074531d470d789fba2bca
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="validation-master-data-services"></a>Validación (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], los datos se validan para asegurarse de su precisión. Cierta validación se realiza automáticamente, mientras que otra se basa en las reglas de negocios creadas por los administradores.  
  
## <a name="when-data-validation-occurs"></a>Cuándo se produce la validación de datos  
 La validación se produce en momentos diferentes y se muestra de forma distinta en la aplicación web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
|Tipo de validación|Estándares determinados por|Cuándo se produce|Se muestra en la interfaz de usuario web de Master Data Manager como|Se muestra en el complemento de Excel como|¿Se guardan los datos en el repositorio MDS?|  
|---------------------|-----------------------------|--------------------|---------------------------------------------------|-------------------------------------------|------------------------------------------|  
|Validación de la regla de negocios|Un administrador de MDS|Automáticamente cuando un usuario agrega o edita datos.<br /><br /> Manualmente cuando un usuario aplica reglas de negocios.<br /><br /> Manualmente cuando un administrador en el área funcional **Administración de versiones** de la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] valida una versión comparándola con las reglas de negocios.|Errores de validación|ValidationStatus|Sí|  
|Validación del tipo de datos y el contenido|Un administrador de MDS, al crear objetos de modelo (por ejemplo, la longitud o el tipo de datos de un atributo)|Automáticamente cuando un usuario agrega o edita datos|Errores de entrada|InputStatus|No|  
|Validación del tipo de datos y el contenido|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o bien [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|Automáticamente cuando un usuario agrega o edita datos|Errores de entrada|InputStatus|No|  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear reglas de negocios y publicarlas para validar los datos con ellas.|[Crear y publicar una regla de negocios &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)|  
|Validar una versión de datos según las reglas de negocios. Solo los administradores.|[Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)|  
|Validar subconjuntos específicos de datos según las reglas de negocios. Todos los usuarios con permiso en el área funcional **Explorador** .|[Validar miembros específicos con las reglas de negocios &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)|  
|Validar subconjuntos específicos de datos según las reglas de negocios. Todos los usuarios con permiso en el área funcional **Explorador** que usen [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].|[Aplicar reglas de negocios &#40;complemento MDS para Excel&#41;](../master-data-services/microsoft-excel-add-in/apply-business-rules-mds-add-in-for-excel.md)|  
  
## <a name="see-also"></a>Vea también  
 [Reglas de negocios &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
