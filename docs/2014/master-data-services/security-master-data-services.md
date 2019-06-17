---
title: Seguridad (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 56bc41ea-de28-4184-aa7e-99111ae55af5
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 80be0aea6705ed98fd12ea3481af59e289b94604
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482586"
---
# <a name="security-master-data-services"></a>Seguridad (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], use la seguridad para asegurarse de que los usuarios tengan acceso a los datos maestros específicos necesarios para realizar su trabajo y para impedir que tengan acceso a datos que no deben estar disponibles para ellos.  
  
 También puede usar la seguridad para convertir a un usuario en administrador de un modelo concreto y un área funcional (por ejemplo, para permitir que alguien cree versiones del modelo Customer o para ofrecer a alguien la posibilidad de establecer permisos de seguridad).  
  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] se basa en usuarios y grupos de dominio locales o de Active Directory. La seguridad de MDS permite usar un nivel de detalle específico para determinar los datos a los que un usuario puede tener acceso. Debido a la granularidad, la seguridad puede llegar a complicarse fácilmente y debe tener cuidado al usar usuarios y grupos superpuestos. Para obtener más información, consulte [Superponer permisos de usuario y de grupo &#40;Master Data Services&#41;](overlapping-user-and-group-permissions-master-data-services.md).  
  
 Puede asignar acceso de seguridad en el área funcional de **Permisos de usuario y de grupo** de la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] o usando el servicio web.  
  
## <a name="types-of-users"></a>Tipos de usuarios  
 Hay dos tipos de usuarios en [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]:  
  
-   Los que tienen acceso a los datos en el área funcional de **Explorador** .  
  
-   Los que tienen la posibilidad de realizar tareas administrativas en áreas distintas de **Explorador**. Estos usuarios se denominan [Administrators &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
## <a name="how-to-set-security"></a>Cómo establecer la seguridad  
 Para conceder a un usuario o a un grupo permiso de acceso a datos o a la funcionalidad de MDS, debe asignar:  
  
-   [Acceso a áreas funcionales](../../2014/master-data-services/functional-area-permissions-master-data-services.md), que determina a cuál de las cinco áreas funcionales de la interfaz de usuario puede tener acceso un usuario.  
  
-   [Permisos de objeto de modelo](../../2014/master-data-services/model-object-permissions-master-data-services.md), que determinan los atributos a los que puede tener acceso un usuario, y el tipo de acceso (lectura o actualización) que tiene el usuario para esos atributos.  
  
-   Opcionalmente, [permisos de miembros de jerarquía](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md), que determinan los miembros a los que un usuario puede tener acceso, y el tipo de acceso (lectura o actualización) que tiene el usuario para esos miembros.  
  
 Cuando asigna permisos a atributos y miembros, los permisos se cruzan y las reglas determinan qué permiso tiene prioridad. Para obtener más información, consulte [Cómo se determinan los permisos &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md).  
  
 Para implementar la seguridad en el nivel de registro, cree una jerarquía para una entidad y asigne permisos de usuario a los miembros de la jerarquía. Los miembros son registros de datos.  Los permisos de miembros de la jerarquía solo se deberían usar si se desea que un usuario tenga acceso limitado a miembros específicos.  
  
 La siguiente imagen muestra la jerarquía derivada de la entidad estilo y los permisos de miembro de estilo para un usuario seleccionado. Se asignan permisos de actualización a los miembros H {Hombre} y U {Unisex}, y se asignan permisos de solo lectura a los miembros del estilo Mujer. Esto significa que el usuario puede actualizar los registros de los productos para Hombre y Unisex, y solo puede leer los registros de los productos del estilo Mujer.  
  
 ![Permisos de jerarquía derivada y miembro de estilo](../../2014/master-data-services/media/style-derived-hierarchy-mds.png "permisos de jerarquía derivada de estilo y miembro")  
  
 Para obtener información sobre cómo crear una jerarquía, consulte [crear una jerarquía explícita &#40;Master Data Services&#41; ](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md) y [crear una jerarquía derivada &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-derived-hierarchy-master-data-services.md).  
  
 Para obtener información sobre cómo asignar permisos de miembros, vea [asignar permisos de miembro de jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## <a name="security-in-the-add-in-for-excel"></a>Seguridad del complemento de Excel  
 La seguridad establecida en la aplicación web de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] también se aplica a [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]. Los usuarios solo pueden ver y trabajar con datos para los que tienen permiso. Los administradores pueden realizar tareas administrativas.  
  
 La única advertencia es que toda la seguridad asignada en [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] no surtirá efecto en Excel hasta que transcurrido un intervalo de 20 minutos. El intervalo se define mediante la configuración de *MdsMaximumUserInformationCacheInterval* en el archivo web.config. Para cambiar el intervalo, puede cambiar el valor y reiniciar IIS.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Crear un usuario que tenga permiso completo para un modelo.|[Crear un administrador de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-model-administrator-master-data-services.md)|  
|Agregar un grupo de Active Directory a [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]; este es el primer paso para conceder a un grupo permiso de acceso a datos de la aplicación web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|[Agregar un grupo &#40;Master Data Services&#41;](../../2014/master-data-services/add-a-group-master-data-services.md)|  
|Asignar permisos a un área funcional de la aplicación web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|[Asignar permisos del área funcional &#40;Master Data Services&#41;](../../2014/master-data-services/assign-functional-area-permissions-master-data-services.md)|  
|Asignar permisos a los valores de atributo asignando el permiso a los objetos del modelo.|[Asignar permisos de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)|  
|Asignar permisos a los valores de miembro asignando el permiso a los nodos de la jerarquía.|[Asignar los permisos de los miembros de una jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)|  
  
## <a name="see-also"></a>Vea también  
 [Administradores &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)   
 [Usuarios y grupos &#40;Master Data Services&#41;](../../2014/master-data-services/users-and-groups-master-data-services.md)   
 [Permisos del área funcional &#40;Master Data Services&#41;](../../2014/master-data-services/functional-area-permissions-master-data-services.md)   
 [Permisos de objeto del modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [Permisos de miembros de la jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Cómo se determinan los permisos &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
