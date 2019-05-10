---
title: Eliminar un atributo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attributes [Master Data Services], deleting
- deleting attributes [Master Data Services]
ms.assetid: ec3e66f7-0e35-43d7-a80d-64899948ebfe
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: fdf3b766e48843a15e73b7a41b7c434ba604e0af
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65478224"
---
# <a name="delete-an-attribute-master-data-services"></a>Eliminar un atributo (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], elimine un atributo cuando desee eliminar permanentemente el atributo y todos los valores de atributo asociados.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso para tener acceso al área funcional de **Administración del sistema** .  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-an-attribute"></a>Para eliminar un atributo  
  
1.  En [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], haga clic en **Administración del sistema**.  
  
2.  En la página **Manage Model** (Administrar modelo), seleccione un modelo de la cuadrícula y después haga clic en **Entidades**.  
  
3.  En la página **Manage Entity** (Administrar entidad), seleccione la fila de la entidad para la que desea crear un atributo.  
  
4.  Haga clic en **Atributos**.  
  
5.  En la página **Administrar atributos** , realice una de las siguientes acciones.  
  
    -   Si el atributo es para miembros hoja, seleccione **Hoja** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
    -   Si el atributo es para miembros consolidados, seleccione **Consolidado** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
    -   Si el atributo es para colecciones, seleccione **Colección** en el cuadro de lista **Member Types** (Tipos de miembro).  
  
6.  Seleccione la fila para el atributo que desea eliminar.  
  
    > [!NOTE]  
    >  No puede eliminar los atributos Code o Name.  
  
7.  Haga clic en **Eliminar**.  
  
8.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)   
 [Atributos basados en dominios &#40;Master Data Services&#41;](../master-data-services/domain-based-attributes-master-data-services.md)   
 [Crear un atributo de texto &#40;Master Data Services&#41;](../master-data-services/create-a-text-attribute-master-data-services.md)   
 [Crear un atributo basado en dominio &#40;Master Data Services&#41;](../master-data-services/create-a-domain-based-attribute-master-data-services.md)  
  
  
