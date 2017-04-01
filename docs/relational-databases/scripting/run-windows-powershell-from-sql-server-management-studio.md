---
title: "Ejecutar Windows PowerShell desde SQL Server Management Studio | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Ejecutar Windows PowerShell desde SQL Server Management Studio
  Puede iniciar sesiones de Windows PowerShell desde el **Explorador de objetos** en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] inicia Windows PowerShell, carga el módulo **sqlps** y establece el contexto de ruta de acceso al nodo asociado en el árbol del **Explorador de objetos**.  
  
## Antes de empezar  
 Al especificar la ejecución de PowerShell para un objeto en el **Explorador de objetos**, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inicia una sesión de Windows PowerShell en la que los complementos PowerShell de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se han cargado y registrado. La ruta de acceso para la sesión se preestablece en la ubicación del objeto en el que hizo clic con el botón secundario en el Explorador de objetos. Por ejemplo, si hace clic con el botón derecho en el objeto de base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en el Explorador de objetos y selecciona **Iniciar PowerShell**, la ruta de acceso de Windows PowerShell se establece en lo siguiente:  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## Ejecutar PowerShell  
 **Para ejecutar PowerShell desde SQL Server Management Studio**  
  
1.  Abra el **Explorador de objetos**.  
  
2.  Navegue al nodo del objeto en el que trabajará.  
  
3.  Haga clic con el botón derecho en el objeto y seleccione **Iniciar PowerShell**.  
  
## Permisos  
 Cuando se abre desde [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], PowerShell no se ejecuta con privilegios de Administrador, lo que puede impedir algunas actividades como llamadas a WMI.  
  
## Vea también  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  