---
title: Seguimiento de cambios (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- change tracking [SQL Server]
ms.assetid: 5e879c65-0d38-454f-9a20-62a6e72c89f7
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a4092257bb593439ef4851eca8b554f0f5ae7ade
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972005"
---
# <a name="change-tracking-master-data-services"></a>Seguimiento de cambios [Master Data Services]
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], puede usar grupos de seguimiento de cambios para realizar una acción cuando cambie un valor de atributo. Use el seguimiento de cambios cuando no conozca cuál será el nuevo valor, pero quiera saber si se produjo algún cambio.  
  
## <a name="configuring-change-tracking"></a>Configurar el seguimiento de cambios  
 Para configurar el seguimiento de cambios, agregue un atributo a un grupo de seguimiento de cambios. El grupo puede contener uno o muchos atributos. A continuación, cree una regla de negocios para definir la acción que se realizará cuando alguno de los atributos del grupo cambie.  
  
> [!NOTE]  
>  Las reglas de negocios del seguimiento de cambios consideran los cambios en lo datos almacenados (importados) provisionalmente.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Agregar atributos a un grupo de seguimiento de cambios.|[Agregar atributos a un grupo de seguimiento de cambios &#40;Master Data Services&#41;](add-attributes-to-a-change-tracking-group-master-data-services.md)|  
|Crear una regla de negocios para iniciar acciones según los cambios en los atributos.|[Iniciar acciones según los cambios de valores de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/initiate-actions-based-on-attribute-value-changes-master-data-services.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
  
-   [Validación &#40;Master Data Services&#41;](../../2014/master-data-services/validation-master-data-services.md)  
  
-   [Reglas de negocios &#40;Master Data Services&#41;](../../2014/master-data-services/business-rules-master-data-services.md)  
  
-   [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
