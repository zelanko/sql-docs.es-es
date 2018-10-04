---
title: Dominios de aplicación y seguridad de la integración de CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- application domains [CLR integration]
ms.assetid: 54ee904e-e21a-4ee7-b4ad-a6f6f71bd473
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 34814ab19f96ff7e6232638ef4446b05b5b41ba3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102355"
---
# <a name="application-domains-and-clr-integration-security"></a>Dominios de aplicación y seguridad de la integración CLR
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carga ensamblados que pertenecen al mismo propietario en el mismo dominio de aplicación. En virtud de un conjunto de ensamblados que se ejecutan en el mismo dominio de aplicación, los ensamblados pueden detectarse entre sí en tiempo de ejecución mediante las interfaces de programación de aplicaciones de reflexión de .NET Framework u otros recursos y pueden realizar llamadas en ellos en modo de enlace en tiempo de ejecución. Dado que tales llamadas se producen en ensamblados que pertenecen al mismo propietario, en ellas no se compruebe ningún permiso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El esquema de ubicación de los ensamblados en los dominios de aplicación se ha diseñado principalmente para lograr los objetivos de escalabilidad, seguridad y aislamiento y es posible que cambie en futuras versiones. Por lo tanto, no debe depender de la localización de ensamblados en el mismo dominio de aplicación a través de los mecanismos de enlace en tiempo de ejecución.  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de la integración CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
