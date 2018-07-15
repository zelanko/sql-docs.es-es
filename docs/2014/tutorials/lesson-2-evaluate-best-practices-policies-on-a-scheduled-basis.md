---
title: 'Lección 2: Evaluar las directivas de prácticas recomendadas de forma programada | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 37ffad63-d6db-4609-8deb-786200659554
caps.latest.revision: 4
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: bfdad3793673e24ddf87d504ab71c96c0bac16f9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196605"
---
# <a name="lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis"></a>Lección 2: evaluar las directivas de las prácticas recomendadas de forma programada
  Puede configurar evaluaciones programadas de directivas de prácticas recomendadas en una o más instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para configurar las directivas de prácticas recomendadas de modo que se ejecuten de forma programada, debe importar las directivas en la instancia de destino.  
  
 Para implementar las directivas programadas en varios servidores, puede importarlas en una instancia, configurar las programaciones de cada directiva, exportar las directivas programadas en una carpeta y, a continuación, implementarlas de modo que se destinen a las instancias a través de servidores registrados.  
  
> [!IMPORTANT]  
>  Las instancias de destino deben ejecutar [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] o una versión posterior. La automatización requiere que las directivas estén almacenadas localmente en la instancia, lo que no se admite en versiones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
 En esta lección, hará lo siguiente:  
  
-   Importar las directivas de prácticas recomendadas en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Configurar las directivas para ejecutarse según una programación.  
  
-   Implementar las directivas de prácticas recomendadas programadas en varias instancias mediante servidores registrados.  
  
 En esta lección se incluyen los temas siguientes:  
  
-   [Importar las directivas a una instancia única](../../2014/tutorials/import-the-policies-to-a-single-instance.md)  
  
-   [Programar las directivas](../../2014/tutorials/schedule-the-policies.md)  
  
-   [Implementar directivas programadas en varias instancias](../../2014/tutorials/deploy-scheduled-policies-to-multiple-instances.md)  
  
## <a name="see-also"></a>Vea también  
 [Administrar varios servidores mediante Servidores de administración central](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
