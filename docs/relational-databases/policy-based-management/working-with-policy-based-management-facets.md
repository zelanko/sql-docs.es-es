---
title: Trabajar con facetas de administración basadas en directivas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- viewing Policy-Based Management facets
- facets [Policy-Based Management], copying
- facets [Policy-Based Management], viewing
- copying Policy-Based Management facets
ms.assetid: 88d025c4-07c2-4e4d-8634-204249a8c82c
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 74d168321d2ef50d444e380b288044725bf16f8f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="working-with-policy-based-management-facets"></a>Trabajar con facetas de administración basada en directivas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Una faceta de administración basada en directivas es un conjunto de propiedades lógicas que se relacionan con una área de interés de administración. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye varias facetas predefinidas. Por ejemplo, la faceta Configuración de área expuesta define, como propiedades, las características que están desactivadas de forma predeterminada.  
  
 Al administrar varios entornos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] similares, puede configurar una faceta en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], copiar el estado de la faceta en un archivo y, a continuación, importar ese archivo en otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como una directiva. Cuando el estado se ha convertido en una directiva, la directiva se puede aplicar a otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], objetos de instancia, bases de datos u objetos de base de datos.  
  
 En este tema se describe cómo copiar el estado de una faceta en un archivo XML.  
  
##  <a name="BeforeYouBegin"></a> Permisos  
 Los procedimientos descritos en este tema requieren la pertenencia al rol PolicyAdministratorRole de la base de datos msdb.  
  
## <a name="viewing-and-copying-facet-states"></a>Ver y copiar los estados de la faceta  
 [Ver las facetas de administración basada en directivas en un objeto de SQL Server](../../relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md)  
  
 [Copiar en un archivo XML un estado de faceta de administración basada en directivas](../../relational-databases/policy-based-management/copy-a-policy-based-management-facet-state-to-an-xml-file.md)  
  
## <a name="see-also"></a>Ver también  
 [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
