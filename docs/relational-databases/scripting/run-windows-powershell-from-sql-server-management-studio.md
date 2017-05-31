---
title: Ejecutar Windows PowerShell desde SQL Server Management Studio | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ec4be68684d53bc8252c0c08e51a47eccb0cc05d
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>Ejecutar Windows PowerShell desde SQL Server Management Studio
  Puede iniciar sesiones de Windows PowerShell desde el **Explorador de objetos** en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] inicia Windows PowerShell, carga el módulo **sqlps** y establece el contexto de ruta de acceso al nodo asociado en el árbol del **Explorador de objetos** .  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Al especificar la ejecución de PowerShell para un objeto en el **Explorador de objetos**, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inicia una sesión de Windows PowerShell en la que los complementos PowerShell de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se han cargado y registrado. La ruta de acceso para la sesión se preestablece en la ubicación del objeto en el que hizo clic con el botón secundario en el Explorador de objetos. Por ejemplo, si hace clic con el botón derecho en el objeto de base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] en el Explorador de objetos y selecciona **Iniciar PowerShell**, la ruta de acceso de Windows PowerShell se establece en lo siguiente:  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="run-powershell"></a>Ejecutar PowerShell  
 **Para ejecutar PowerShell desde SQL Server Management Studio**  
  
1.  Abra el **Explorador de objetos**.  
  
2.  Navegue al nodo del objeto en el que trabajará.  
  
3.  Haga clic con el botón derecho en el objeto y seleccione **Iniciar PowerShell**.  
  
## <a name="permissions"></a>Permisos  
 Cuando se abre desde [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], PowerShell no se ejecuta con privilegios de Administrador, lo que puede impedir algunas actividades como llamadas a WMI.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
