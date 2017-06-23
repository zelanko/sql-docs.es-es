---
title: "Descargar el módulo de PowerShell SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- instalar sql server powershell, descargue sql server powershell
ms.assetid: 
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: f55266b6ec28e2552047cc36a5060945006b2caa
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="download-sql-server-powershell-module"></a>Descargar el módulo de PowerShell SQL Server
Como parte de la versión 17.0 de SQL Server Management Studio, el módulo de PowerShell de SQL Server ahora se distribuye a través de la Galería de PowerShell.  El módulo ya no se incluye en el paquete de instalación SSMS. Para usar PowerShell con SSMS 17,0 y versiones más recientes, el módulo de SQL Server debe instalarse en el equipo como un paso adicional.

Completa la documentación acerca de cómo instalar la versión más reciente de Windows Management Framework y cómo instalar los módulos de PowerShell en general puede encontrarse en el [Galería de PowerShell](https://www.powershellgallery.com/) sitio.

El comando de PowerShell para instalar el módulo de SQL Server es:

> Install-module-nombre SqlServer-ámbito CurrentUser

Si hay versiones anteriores de los módulos de PowerShell de SQL Server en el equipo, es posible que sea necesario proporcionar el "-AllowClobber" parámetro.  

Las versiones del módulo de PowerShell de SQL Server que se van a enviar a la Galería de PowerShell admiten las versiones y requieren PowerShell versión 5.0 o posterior.

