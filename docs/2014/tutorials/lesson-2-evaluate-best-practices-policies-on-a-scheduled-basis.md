---
title: 'Lección 2: evaluar las directivas de prácticas recomendadas de forma programada | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 37ffad63-d6db-4609-8deb-786200659554
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 29513ec37a946b9ec613ccc483048396149dd15a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63042688"
---
# <a name="lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis"></a>Lección 2: Evaluación de las directivas de procedimientos recomendados de forma programada
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
  
## <a name="see-also"></a>Consulte también  
 [Administrar varios servidores mediante Servidores de administración central](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
