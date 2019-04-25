---
title: Jerarquías derivadas con límites explícitos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services], derived hierarchies with explicit caps
- explicit hierarchies, derived hierarchies with explicit caps
- derived hierarchies, derived hierarchies with explicit caps
ms.assetid: 6a82ff66-c137-4757-99bb-787d189b4295
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 89b4eccbe26817d25d8c80a56e602fcbc5ab6e8a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62765658"
---
# <a name="derived-hierarchies-with-explicit-caps-master-data-services"></a>Jerarquías derivadas con límites explícitos (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], el hecho de que los niveles de una jerarquía explícita se utilicen como niveles superiores de una jerarquía derivada, se denomina jerarquía derivada con límites explícitos.  
  
 La jerarquía explícita debe estar basada en la misma entidad que la entidad del nivel superior de la jerarquía derivada.  
  
 En la interfaz de usuario de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , para crear este tipo de jerarquía, arrastre una jerarquía explícita hasta la parte superior de una jerarquía derivada.  
  
 ![mds_conc_explicit_cap_UI_structure](../../2014/master-data-services/media/mds-conc-explicit-cap-ui-structure.gif "mds_conc_explicit_cap_UI_structure")  
  
## <a name="derived-hierarchy-with-explicit-cap-example"></a>Ejemplo de jerarquía derivada con límite explícito  
 En este ejemplo, los miembros de la jerarquía explícita son los de la entidad Subcategory. En la jerarquía derivada, los miembros de nivel superior también son los de la entidad Subcategory.  
  
 ![mds_conc_explicit_cap_UI_example](../../2014/master-data-services/media/mds-conc-explicit-cap-ui-example.gif "mds_conc_explicit_cap_UI_example")  
  
 Al usar la jerarquía explícita en el nivel superior de una jerarquía derivada, la jerarquía derivada queda desigual.  
  
## <a name="rules"></a>Reglas  
  
-   No puede tener más de una jerarquía explícita en una jerarquía derivada con límites explícitos.  
  
-   Puede utilizar la misma jerarquía explícita como límite para varias jerarquías derivadas.  
  
-   No puede asignar permisos a los miembros de jerarquías derivadas con límites explícitos. Si asigna individualmente permisos a la jerarquía explícita o a la jerarquía derivada, los permisos afectan a ambas.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear una jerarquía derivada.|[Crear una jerarquía derivada &#40;Master Data Services&#41;](create-a-derived-hierarchy-master-data-services.md)|  
|Crear una jerarquía explícita.|[Crear una jerarquía explícita &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)|  
|Eliminar una jerarquía derivada existente.|[Eliminar una jerarquía derivada &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
|||  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Jerarquías derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
-   [Jerarquías explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
