---
title: Crear una jerarquía derivada (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies, creating
- creating derived hierarchies [Master Data Services]
ms.assetid: fec653c4-11cc-46a2-8dd8-b605341ebb40
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 0b56342c407bf2324da503810ca00d797b1c5cc6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782377"
---
# <a name="create-a-derived-hierarchy-master-data-services"></a>Crear una jerarquía derivada (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], cree una jerarquía derivada cuando desee una jerarquía basada en nivel que garantice que los miembros existen en el nivel correcto. Las jerarquías derivadas se basan en las relaciones de atributo basados en dominios que existen en un modelo.  
  
> [!NOTE]  
>  Si un valor de atributo basado en dominios no existe para un miembro, este no se incluye en la jerarquía derivada. Consulte [Requerir valores de atributo &#40;Master Data Services&#41;](require-attribute-values-master-data-services.md) para requerir un valor de atributo basado en dominio para todos los miembros.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-a-derived-hierarchy"></a>Crear una jerarquía derivada  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En el **vista de modelo** página, en la barra de menús, seleccione **administrar** y haga clic en **jerarquías derivadas**.  
  
3.  En la página **Mantenimiento de jerarquías derivadas** , en la lista **Modelo** , seleccione un modelo.  
  
4.  Haga clic en **agregar jerarquía derivada**.  
  
5.  En la página **Agregar jerarquía derivada** , en el cuadro **Nombre de jerarquía derivada** , escriba un nombre para la jerarquía.  
  
    > [!TIP]  
    >  Use un nombre que describa los niveles de la jerarquía, por ejemplo **Producto de subcategoría a categoría**.  
  
6.  Haga clic en **Guardar jerarquía derivada**.  
  
7.  En el **Editar jerarquía derivada** página, en el **entidades y jerarquías disponibles** panel, haga clic en una entidad o jerarquía y arrástrelo hasta el **niveles actuales** panel.  
  
8.  Siga arrastrando entidades o jerarquías hasta que la jerarquía esté completa.  
  
9. Haga clic en **Atrás**.  
  
## <a name="see-also"></a>Vea también  
 [Jerarquías derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [Jerarquías derivadas con límites explícitos &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [Atributos basados en dominios &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)  
  
  
