---
title: Instalar SQL Server PowerShell | Microsoft Docs
ms.custom: 
ms.date: 02/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 795a19f9f9d3c357d972197736687628ee2ac51d
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="install-sql-server-powershell"></a>Instalar SQL Server PowerShell
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El programa de instalación configura automáticamente los componentes de PowerShell.  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-powershell-support"></a>Instalar compatibilidad con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell  
 Debe instalar el software que proporciona compatibilidad con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Windows PowerShell utilizando el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando selecciona cualquier característica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que requiera compatibilidad con PowerShell, el programa de instalación instala los siguientes componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell:  
  
-   Los complementos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Los complementos son archivos DLL que implementan dos tipos de compatibilidad con Windows PowerShell para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   Un conjunto de cmdlets de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los cmdlets son comandos que implementan una acción concreta. Por ejemplo, **Invoke-Sqlcmd** ejecuta un script de [!INCLUDE[tsql](../../includes/tsql-md.md)] o XQuery que también se puede ejecutar mediante la utilidad **sqlcmd** e **Invoke-PolicyEvaluation** notifica si los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cumplen las directivas de administración basada en directivas.  
  
    -   Un proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El proveedor permite navegar por la jerarquía de objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando una ruta de acceso similar a una ruta de acceso al sistema de archivos. Cada objeto se asocia a una clase de los modelos de objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Puede utilizar los métodos y las propiedades de la clase para realizar un trabajo en los objetos. Por ejemplo, si cambia el directorio a un objeto de bases de datos en una ruta de acceso, puede utilizar los métodos y las propiedades de la clase Microsoft.SqlServer.Managment.SMO.Database para administrar la base de datos.  
  
-   El módulo **sqlps** que se importa en las sesiones de Windows PowerShell para cargar complementos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] admite el inicio de sesiones de Windows PowerShell desde el árbol del Explorador de objetos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es compatible con los pasos de trabajo de Windows PowerShell.  
  
 Windows Server 2012 y versiones posteriores y Windows 8 y versiones posteriores incluyen PowerShell instalado y configurado. Para obtener información sobre cómo instalar Windows PowerShell, vea la página [Instalación de Windows PowerShell](http://msdn.microsoft.com/library/hh847837.aspx) .  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  

