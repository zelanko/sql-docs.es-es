---
title: Dominios de aplicación y seguridad de la integración CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- application domains [CLR integration]
ms.assetid: 54ee904e-e21a-4ee7-b4ad-a6f6f71bd473
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 85d6e66b1d51cc9d7c5829b8e83c510bea750e2a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933767"
---
# <a name="application-domains-and-clr-integration-security"></a>Dominios de aplicación y seguridad de la integración CLR
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carga ensamblados que pertenecen al mismo propietario en el mismo dominio de aplicación. En virtud de un conjunto de ensamblados que se ejecutan en el mismo dominio de aplicación, los ensamblados pueden detectarse entre sí en tiempo de ejecución mediante las interfaces de programación de aplicaciones de reflexión de .NET Framework u otros recursos y pueden realizar llamadas en ellos en modo de enlace en tiempo de ejecución. Dado que tales llamadas se producen en ensamblados que pertenecen al mismo propietario, en ellas no se compruebe ningún permiso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El esquema de ubicación de los ensamblados en los dominios de aplicación se ha diseñado principalmente para lograr los objetivos de escalabilidad, seguridad y aislamiento y es posible que cambie en futuras versiones. Por lo tanto, no debe depender de la localización de ensamblados en el mismo dominio de aplicación a través de los mecanismos de enlace en tiempo de ejecución.  
  
## <a name="see-also"></a>Consulte también  
 [Seguridad de la integración CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
