---
title: Quitar componentes de SQL Server Data Tools | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: f8ddb919-661f-4868-8c71-87c96f1f4487
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6b114b99b816e10bc004cea8d60c56d296053c7c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685473"
---
# <a name="removing-sql-server-data-tools-components"></a>Quitar componentes de SQL Server Data Tools
Algunos componentes de SQL Server Data Tools (SSDT) no se quitan al desinstalar SSDT o Visual Studio.  
  
Los siguientes paquetes de Windows Installer (.msi) no se quitarán del equipo cuando se desinstale SSDT o Visual Studio. Al quitar estos componentes, las demás versiones de Visual Studio pueden quedar en un estado no compatible. Si decide quitar estos componentes, use Agregar o quitar programas de Windows:  
  
-   MicrosoftSQL Server Data Tools (SSDT.msi)  
  
-   Utilidades de compilación de MicrosoftSQL Server Data Tools (SSDTBuildUtilities.msi)  
  
-   Requisitos previos para SSDT (SSDTDBSvcExternals.msi)  
  
Otros productos pueden usar los siguientes componentes compartidos y continuarán en el equipo después de que se desinstale SSDT.  
  
-   Marco de trabajo de la aplicación de capa de datos de SQL Server (DACFramework.msi)  
  
-   Objetos de administración de SQL Server (SharedManagementObjects.msi)  
  
-   Servicio de lenguaje de SQL Server Transact\-SQL (TSqlLanguageService.msi)  
  
-   MicrosoftSQL Server System CLR Types para SQL Server (SQLSysClrTypes.msi)  
  
-   SQL ServerTransact\-SQL ScriptDom (SQLDom.msi)  
  
-   SQL ServerTransact\-SQL Compiler Service (SQLLs.msi)  
  
