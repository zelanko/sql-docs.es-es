---
title: Servicios de acceso a la integración | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SSIS packages, security
- viewing packages while running
- displaying packacges while running
- security [Integration Services], running packages
- packages [Integration Services], security
- current packages running
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 1088aafc-14c5-4e7d-9930-606a24c3049b
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6fdae3756442b1af660095fe53cbc8e4e3db82da
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106157"
---
# <a name="access-to-the-integration-services-service"></a>Acceso al servicio Integration Services
  Los niveles de protección de paquetes pueden limitar quién puede editar y ejecutar un paquete. Es necesaria protección adicional para limitar quién puede ver la lista de paquetes actualmente en ejecución en un servidor y quién puede detener dicha ejecución en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] utiliza el servicio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para mostrar los paquetes que se están ejecutando. Los miembros del grupo Administradores de Windows pueden ver y detener todos los paquetes en ejecución. Los usuarios que no sean miembros del grupo Administradores solo pueden ver y detener los paquetes que han iniciado ellos mismos.  
  
 Es importante restringir el acceso a los equipos que ejecutan un servicio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , especialmente un servicio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que puede mostrar carpetas remotas. Cualquier usuario autenticado puede solicitar la enumeración de los paquetes. Aunque el servicio encuentre el servicio, el servicio enumera las carpetas. Estos nombres de carpeta pueden ser útiles para un usuario malintencionado. Si un administrador configura el servicio para que enumere las carpetas en un equipo remoto, los usuarios también podrán ver los nombres de las carpetas que normalmente no podrían ver.  
  
  