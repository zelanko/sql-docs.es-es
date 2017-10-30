---
title: "Jerarquías derivadas con límites explícitos (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchies [Master Data Services], derived hierarchies with explicit caps
- explicit hierarchies, derived hierarchies with explicit caps
- derived hierarchies, derived hierarchies with explicit caps
ms.assetid: 6a82ff66-c137-4757-99bb-787d189b4295
caps.latest.revision: 7
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 811aa84b91aa7c91aa56dbf231c2ef2d247ec015
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="derived-hierarchies-with-explicit-caps-master-data-services"></a>Jerarquías derivadas con límites explícitos (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], el hecho de que los niveles de una jerarquía explícita se utilicen como niveles superiores de una jerarquía derivada, se denomina jerarquía derivada con límites explícitos.  
  
 La jerarquía explícita debe estar basada en la misma entidad que la entidad del nivel superior de la jerarquía derivada.  
  
 En la interfaz de usuario de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , para crear este tipo de jerarquía, arrastre una jerarquía explícita hasta la parte superior de una jerarquía derivada.  
  
 ![mds_conc_explicit_cap_UI_structure](../master-data-services/media/mds-conc-explicit-cap-ui-structure.gif "mds_conc_explicit_cap_UI_structure")  
  
## <a name="derived-hierarchy-with-explicit-cap-example"></a>Ejemplo de jerarquía derivada con límite explícito  
 En este ejemplo, los miembros de la jerarquía explícita son los de la entidad Subcategory. En la jerarquía derivada, los miembros de nivel superior también son los de la entidad Subcategory.  
  
 ![mds_conc_explicit_cap_UI_example](../master-data-services/media/mds-conc-explicit-cap-ui-example.gif "mds_conc_explicit_cap_UI_example")  
  
 Al usar la jerarquía explícita en el nivel superior de una jerarquía derivada, la jerarquía derivada queda desigual.  
  
## <a name="rules"></a>Reglas  
  
-   No puede tener más de una jerarquía explícita en una jerarquía derivada con límites explícitos.  
  
-   Puede utilizar la misma jerarquía explícita como límite para varias jerarquías derivadas.  
  
-   No puede asignar permisos a los miembros de jerarquías derivadas con límites explícitos. Si asigna individualmente permisos a la jerarquía explícita o a la jerarquía derivada, los permisos afectan a ambas.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear una jerarquía derivada.|[Crear una jerarquía derivada &#40;Master Data Services&#41;](../master-data-services/create-a-derived-hierarchy-master-data-services.md)|  
|Crear una jerarquía explícita.|[Crear una jerarquía explícita &#40;Master Data Services&#41;](../master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Eliminar una jerarquía derivada existente.|[Eliminar una jerarquía derivada &#40;Master Data Services&#41;](../master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
|||  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Jerarquías derivadas &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
-   [Jerarquías explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
  

