---
title: Jerarquías recursivas (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- recursive hierarchies [Master Data Services]
- hierarchies [Master Data Services], recursive hierarchies
ms.assetid: 9408c6ea-d9c4-4a0b-8a1b-1457fb6944af
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0ebe093973174fe1e245ced134888d3e10417467
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65478839"
---
# <a name="recursive-hierarchies-master-data-services"></a>Jerarquías recursivas (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], una jerarquía recursiva es una jerarquía derivada que incluye una relación recursiva. Una relación recursiva existe cuando una entidad tiene un atributo basado en dominio en la propia entidad.  
  
## <a name="recursive-hierarchy-example"></a>Ejemplo de jerarquía recursiva  
 Un ejemplo de jerarquía recursiva típica es una estructura organizativa. En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], esto se haría creando una entidad Empleado con un atributo basado en dominio llamado Administrador. El atributo Administrador se rellena a partir de la lista de empleados. En esta organización de ejemplo, todos los empleados pueden ser administradores.  
  
 ![mds_conc_recursive_table_w_data](../../2014/master-data-services/media/mds-conc-recursive-table-w-data.gif "mds_conc_recursive_table_w_data")  
  
 Puede crear una jerarquía derivada que resalte la relación entre la entidad Empleado y el atributo basado en dominio Administrador.  
  
 ![mds_conc_recursive_UI_structure](../../2014/master-data-services/media/mds-conc-recursive-ui-structure.gif "mds_conc_recursive_UI_structure")  
  
 Para incluir cada miembro en la jerarquía solo una vez, puede delimitar las relaciones nulas. Cuando se hace esto, los miembros con los valores de atributo basado en dominio en blanco se muestran en el nivel superior de la jerarquía.  
  
 ![mds_conc_recursive_UI_example_anchored](../../2014/master-data-services/media/mds-conc-recursive-ui-example-anchored.gif "mds_conc_recursive_UI_example_anchored")  
  
 Si no delimita las relaciones nulas, los miembros se incluyen varias veces. Todos los miembros se muestran en el nivel superior. También se muestran bajo los miembros de los que son atributos.  
  
 ![mds_conc_recursive_UI_example_nonanchored](../../2014/master-data-services/media/mds-conc-recursive-ui-example-nonanchored.gif "mds_conc_recursive_UI_example_nonanchored")  
  
 En este ejemplo, Marcia está en el nivel superior. No es la administradora de ningún empleado porque no se utiliza como valor de atributo basado en dominio para ningún otro miembro Empleado. Robert, por el contrario, tiene un nivel por debajo porque Marcia tiene a Robert como valor de su atributo Administrador.  
  
## <a name="rules"></a>Reglas  
  
-   Una jerarquía derivada no puede contener más de una relación recursiva. Sin embargo, puede tener otras relaciones derivadas (por ejemplo, una jerarquía derivada que contenga una relación recursiva entre administrador y empleado también puede tener relaciones entre país y administrador y entre empleado y almacén).  
  
-   No puede asignar permisos de miembro (en la pestaña **Miembros de la jerarquía** ) a los miembros de una jerarquía recursiva.  
  
-   Las jerarquías recursivas no pueden incluir relaciones circulares. Por ejemplo, Katherine no puede ser administradora de Sandeep si este es su administrador. Asimismo, Katherine no se puede administrar así misma.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear una jerarquía derivada.|[Cree una jerarquía derivada &#40;Master Data Services&#41;](create-a-derived-hierarchy-master-data-services.md)|  
|Cambiar el nombre de una jerarquía derivada existente.|[Cambiar el nombre de una jerarquía derivada &#40;Master Data Services&#41;](../../2014/master-data-services/change-a-derived-hierarchy-name-master-data-services.md)|  
|Eliminar una jerarquía derivada existente.|[Eliminar una jerarquía derivada &#40;Master Data Services&#41;](../../2014/master-data-services/delete-a-derived-hierarchy-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Atributos basados en dominio &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)  
  
-   [Jerarquías derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
  
