---
title: Crear un miembro de hoja (Master Data Services) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- leaf members [Master Data Services], creating
- creating leaf members [Master Data Services]
- members [Master Data Services], creating leaf members
ms.assetid: 0499d3b3-d508-4d43-a740-19cf53ade9f1
caps.latest.revision: 14
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3745604313dde3eda55c3d0f5d8f634bf7187440
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-leaf-member-master-data-services"></a>Crear un miembro hoja (Master Data Services)
  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], cree un miembro hoja si desea agregar datos maestros al sistema. Si desea agregar datos de forma masiva, use tablas de almacenamiento provisional. Para obtener más información, consulte [Importar datos de tablas &#40;Master Data Services&#41;](../master-data-services/import-data-from-tables-master-data-services.md)  
  
 También puede usar [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] para importar datos.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
-   Como mínimo, debe tener el permiso **Crear** o **Actualizar** para el objeto de modelo hoja en la entidad a la que vaya a agregar un miembro. El permiso Crear le permite crear un miembro y modificar solo el atributo de código. El permiso Actualizar le permite actualizar otros atributos.  
  
     Para obtener más información, consulte [Seguridad &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md).  
  
### <a name="to-create-a-leaf-member"></a>Crear un miembro hoja  
  
1.  En la página principal de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , en la lista **Modelo** , seleccione un modelo.  
  
2.  Si es un usuario, seleccione una versión abierta de la lista **Versión** . Si es administrador, seleccione una versión que tenga el estado abierto o bloqueado de la lista **Versión** .  
  
3.  Haga clic en **Explorador**.  
  
4.  En la barra de menús, seleccione **Entidades** y haga clic en el nombre de la entidad a la que desee agregar un miembro.  
  
5.  Haga clic en **Agregar miembro**.  
  
6.  En el panel **Detalles** , cumplimente los campos.  
  
     Si un atributo está basado en dominio y se ha aplicado un filtro al atributo, se restringirá la lista de valores de atributo en función del atributo primario de filtro.  
  
     Para obtener más información sobre los atributos primarios de filtro y basados en dominio, consulte [Crear un atributo basado en dominio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
7.  Opcional. En el cuadro **Anotaciones** , escriba un comentario sobre los motivos por los que se agregó el miembro. Todos los usuarios que tienen acceso al miembro pueden ver la anotación.  
  
8.  Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Crear un miembro consolidado &#40;Master Data Services&#41;](../master-data-services/create-a-consolidated-member-master-data-services.md)   
 [Los miembros &#40; Master Data Services &#41;](../master-data-services/members-master-data-services.md)  
  
  
