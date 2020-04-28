---
title: Ejecutar Windows PowerShell desde SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c6d71f1158ef73b84e5b04dcc9a1970bfd7dce35
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783100"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>Ejecutar Windows PowerShell desde SQL Server Management Studio
  Puede iniciar sesiones de Windows PowerShell desde el **Explorador de objetos** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]inicia Windows PowerShell, carga el `sqlps` módulo y establece el contexto de la ruta de acceso en el nodo asociado en el árbol de **Explorador de objetos** .  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Cuando se especifica la ejecución de PowerShell para un **Object Explorer**objeto en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] explorador de objetos, inicia una sesión de Windows PowerShell [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la que los complementos de PowerShell se han cargado y registrado. La ruta de acceso para la sesión se preestablece en la ubicación del objeto en el que hizo clic con el botón secundario en el Explorador de objetos. Por ejemplo, si hace clic con el botón derecho en el objeto de base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] en el Explorador de objetos y selecciona **Iniciar PowerShell**, la ruta de acceso de Windows PowerShell se establece en lo siguiente:  
  
```
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="to-run-powershell-from-sql-server-management-studio"></a>Para ejecutar PowerShell desde SQL Server Management Studio 
  
1.  Abra **Explorador de objetos**.  
  
2.  Navegue al nodo del objeto en el que trabajará.  
  
3.  Haga clic con el botón derecho en el objeto y seleccione **Iniciar PowerShell**.  
  
## <a name="permissions"></a>Permisos  
 Cuando se abre desde [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], PowerShell no se ejecuta con privilegios de Administrador, lo que puede impedir algunas actividades como llamadas a WMI.  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server PowerShell](sql-server-powershell.md)  
