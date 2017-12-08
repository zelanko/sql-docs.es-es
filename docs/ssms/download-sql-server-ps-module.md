---
title: "Descarga del módulo de PowerShell de SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords: instalar powershell de sql server, descargar powershell de sql server
ms.assetid: 
caps.latest.revision: "113"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7f6ab758ecd32d4d9bdb39d9157cbba9b38e73ba
ms.sourcegitcommit: b0c223ba0f78af5eb76948e68e2d1aab2e7b80c1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/16/2017
---
# <a name="download-sql-server-powershell-module"></a>Descarga del módulo de PowerShell de SQL Server
Como parte de la versión 17.0 de SQL Server Management Studio, el módulo de PowerShell de SQL Server ahora se distribuye a través de la Galería de PowerShell.  El módulo ya no se incluye en el paquete de instalación de SSMS. Para usar PowerShell con SSMS 17.0 y versiones más recientes, el módulo de SQL Server debe instalarse en el equipo como paso adicional.

Puede encontrar toda la información sobre cómo instalar la versión más reciente de Windows Management Framework y cómo instalar módulos de PowerShell en general en el sitio de la [Galería de PowerShell](https://www.powershellgallery.com/).

El comando de PowerShell para instalar el módulo de SQL Server es:

> Install-Module -Name SqlServer

Este comando instala el módulo para todos los usuarios del equipo. Debe ejecutar el proceso de PowerShell como administrador.

> Install-Module -Name SqlServer -Scope CurrentUser

Este comando instala el módulo para el usuario que ejecuta el proceso actual de PowerShell. No es necesario ejecutar el proceso de PowerShell con derechos de administrador.

Si hay versiones anteriores de los módulos de PowerShell de SQL Server en el equipo, es posible que haya que proporcionar el parámetro "-AllowClobber".  

Si la ejecución se realiza como administrador y el módulo se instala para todos los usuarios del equipo:

> Install-Module -Name SqlServer -AllowClobber

Si la ejecución no se puede realizar como administrador o la instalación se realiza solo para el usuario actual

> Install-Module -Name SqlServer -Scope CurrentUser -AllowClobber

Si hay versiones actualizadas disponibles del módulo SqlServer, puede actualizar la versión con el comando Update-Module:

> Update-Module -Name SqlServer

Para ver las versiones del módulo instalado en el equipo, puede usar:

> Get-Module SqlServer -ListAvailable

Para usar una versión específica del módulo en los scripts, puede importarla con:

> Import-Module SqlServer -Version 21.0.17178

Las versiones del módulo de PowerShell de SQL Server incluidas en la Galería de PowerShell admiten el control de versiones y requieren la versión 5.0 de PowerShell o una versión posterior. Puede encontrar el módulo SqlServer en la [Galería de PowerShell](https://www.powershellgallery.com/packages/Sqlserver/). 
