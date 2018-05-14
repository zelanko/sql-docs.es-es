---
title: Relación de sincronización de entidades (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bd627a2d-dc64-47e9-9a71-2d0ad04b4962
caps.latest.revision: 6
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: d54b4f3b9211f7ab79483a76c82ec5db14abff72
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="entity-sync-relationship-master-data-services"></a>Relación de sincronización de entidades (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  La sincronización de entidades es una sincronización unidireccional y repetible entre versiones de entidades. Permite compartir datos de entidad entre diferentes modelos. Puede conservar un único origen de confianza en un modelo y volver a usar estos datos maestros en otros modelos. Por ejemplo, puede almacenar los datos de estado de Estados Unidos en la entidad de un modelo y volver a usar esos datos en otros modelos.  
  
 Con la sincronización de entidades, también puede hacer una copia única de los datos.  
  
 Todos los miembros hoja con atributos de archivo y de forma libre en la entidad de origen se sincronizan con la entidad de destino durante la ejecución de la sincronización. Esto permite crear, eliminar y modificar los miembros y esquemas de la entidad.  
  
 Cuando se haya establecido una relación de sincronización, la entidad de destino se puede modificar únicamente mediante el proceso de sincronización. Una relación de sincronización se puede quitar en cualquier momento para que la entidad de destino se pueda modificar.  
  
## <a name="see-also"></a>Ver también  
 [Crear y ejecutar una relación de sincronización de entidades &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [Modificación y eliminación de una relación de sincronización de entidades &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
