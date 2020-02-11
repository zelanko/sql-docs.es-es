---
title: Grupos de cargas de trabajo del regulador de recursos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group
- workload groups [SQL Server]
- workload groups [SQL Server], overview
ms.assetid: a84c3c3f-55b6-4a30-9c42-13f082d9281e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de33dafe9c2274e8e016d619c1e7b5762d73e7aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63209705"
---
# <a name="resource-governor-workload-group"></a>Grupos de cargas de trabajo del regulador de recursos
  En el regulador de recursos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , un grupo de cargas de trabajo actúa como un contenedor de las solicitudes de sesión que tienen criterios de clasificación similares. Una carga de trabajo permite la supervisión agregada de las sesiones y define directivas para estas. Cada grupo de cargas de trabajo está en un grupo de recursos de servidor, que representa un subconjunto de los recursos físicos de una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Cuando se inicia una sesión, el clasificador del regulador de recursos asigna la sesión a un grupo de cargas de trabajo concreto, y la sesión se debe ejecutar utilizando las directivas asignadas al grupo de cargas de trabajo y los recursos definidos para el grupo de recursos de servidor.  
  
## <a name="workload-group-concepts"></a>Conceptos del grupo de cargas de trabajo  
 Un grupo de cargas de trabajo sirve como contenedor para las solicitudes de sesión que sean similares de acuerdo con los criterios de clasificación que se aplican a cada solicitud. Un grupo de cargas de trabajo permite la supervisión agregada del consumo de recursos y la aplicación de una directiva uniforme a todas las solicitudes en el grupo. Un grupo define las directivas para sus miembros.  
  
> [!NOTE]  
>  Los grupos de cargas de trabajo definidos por el usuario se pueden mover de un grupo de recursos de servidor a otro.  
  
 El regulador de recursos predefine dos grupos de cargas de trabajo: el grupo interno y el grupo predeterminado. Un usuario no puede cambiar nada que esté clasificado como grupo interno, pero puede supervisarlo. Las solicitudes se clasifican en el grupo predeterminado cuando se dan las condiciones siguientes:  
  
-   No hay ningún criterio para clasificar una solicitud.  
  
-   Hay un intento de clasificar la solicitud en un grupo inexistente.  
  
-   Hay un error de clasificación general.  
  
 El regulador de recursos también proporciona instrucciones DLL para crear, cambiar y quitar grupos de cargas de trabajo.  
  
## <a name="workload-group-tasks"></a>Tareas de grupo de cargas de trabajo  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo crear un grupo de cargas de trabajo.|[Crear un grupo de cargas de trabajo](create-a-workload-group.md)|  
|Describe cómo cambiar la configuración del grupo de cargas de trabajo.|[Cambiar la configuración del grupo de cargas de trabajo](change-workload-group-settings.md)|  
|Describe cómo eliminar un grupo de cargas de trabajo.|[Eliminar un grupo de cargas de trabajo](delete-a-workload-group.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Regulador de recursos](resource-governor.md)   
 [Habilitar el regulador de recursos](enable-resource-governor.md)   
 [Grupo de recursos de servidor del regulador de recursos](resource-governor-resource-pool.md)   
 [Función clasificadora del regulador de recursos](resource-governor-classifier-function.md)   
 [Configurar el regulador de recursos utilizando una plantilla](configure-resource-governor-using-a-template.md)   
 [Ver las propiedades del regulador de recursos](view-resource-governor-properties.md)  
  
  
