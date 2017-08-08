---
title: "Descarga del módulo de PowerShell de SQL Server | Microsoft Docs"
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
- instalar powershell de sql server, descargar powershell de sql server
ms.assetid: 
caps.latest.revision: 113
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: f55266b6ec28e2552047cc36a5060945006b2caa
ms.contentlocale: es-es
ms.lasthandoff: 07/31/2017

---
# <a name="download-sql-server-powershell-module"></a>Descarga del módulo de PowerShell de SQL Server
Como parte de la versión 17.0 de SQL Server Management Studio, el módulo de PowerShell de SQL Server ahora se distribuye a través de la Galería de PowerShell.  El módulo ya no se incluye en el paquete de instalación de SSMS. Para usar PowerShell con SSMS 17.0 y versiones más recientes, el módulo de SQL Server debe instalarse en el equipo como paso adicional.

Puede encontrar toda la información sobre cómo instalar la versión más reciente de Windows Management Framework y cómo instalar módulos de PowerShell en general en el sitio de la [Galería de PowerShell](https://www.powershellgallery.com/).

El comando de PowerShell para instalar el módulo de SQL Server es:

> Install-module -Name SqlServer -Scope CurrentUser

Si hay versiones anteriores de los módulos de PowerShell de SQL Server en el equipo, es posible que haya que proporcionar el parámetro "-AllowClobber".  

Las versiones del módulo de PowerShell de SQL Server incluidas en la Galería de PowerShell admiten el control de versiones y requieren la versión 5.0 de PowerShell o una versión posterior.

