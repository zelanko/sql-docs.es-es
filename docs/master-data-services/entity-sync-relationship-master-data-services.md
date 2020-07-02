---
title: Relación de sincronización de entidades
description: La sincronización de entidades es una sincronización unidireccional y repetible entre versiones de entidad, lo que permite compartir datos de entidad entre modelos de Master Data Services.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: bd627a2d-dc64-47e9-9a71-2d0ad04b4962
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0dac91e4f43d244e133511e792f29770949da905
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85811950"
---
# <a name="entity-sync-relationship-master-data-services"></a>Relación de sincronización de entidades (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  La sincronización de entidades es una sincronización unidireccional y repetible entre versiones de entidades Permite compartir datos de entidad entre diferentes modelos. Puede conservar un único origen de confianza en un modelo y volver a usar estos datos maestros en otros modelos. Por ejemplo, puede almacenar los datos de estado de Estados Unidos en la entidad de un modelo y volver a usar esos datos en otros modelos.  
  
 Con la sincronización de entidades, también puede hacer una copia única de los datos.  
  
 Todos los miembros hoja con atributos de archivo y de forma libre en la entidad de origen se sincronizan con la entidad de destino durante la ejecución de la sincronización. Esto permite crear, eliminar y modificar los miembros y esquemas de la entidad.  
  
 Cuando se haya establecido una relación de sincronización, la entidad de destino se puede modificar únicamente mediante el proceso de sincronización. Una relación de sincronización se puede quitar en cualquier momento para que la entidad de destino se pueda modificar.  
  
## <a name="see-also"></a>Consulte también  
 [Crear y ejecutar una relación de sincronización de entidades &#40;Master Data Services&#41;](../master-data-services/create-and-execute-an-entity-sync-relationship-master-data-services.md)   
 [Modificación y eliminación de una relación de sincronización de entidades &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-entity-sync-relationship-master-data-services.md)  
  
  
