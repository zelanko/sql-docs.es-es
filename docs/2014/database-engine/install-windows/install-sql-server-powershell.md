---
title: Instalar SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 961f5793732dcfabd19b07f0a22b467591a980c7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203245"
---
# <a name="install-sql-server-powershell"></a>Instalar SQL Server PowerShell
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El programa de instalación se detendrá si detecta que ha seleccionado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] características que incluyen componentes de PowerShell, pero Windows PowerShell 2.0 no está instalado. Debe instalar PowerShell utilizando Windows Management Framework y, a continuación, volver a ejecutar el programa de instalación.  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-powershell-support"></a>Instalar compatibilidad con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell  
 Debe instalar el software que proporciona compatibilidad con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Windows PowerShell utilizando el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al seleccionar cualquier [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten características que requieren PowerShell, el programa de instalación comprueba que Windows PowerShell 2.0 está instalado. Si PowerShell 2.0 está presente, el programa de instalación instala los siguientes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes de PowerShell:  
  
-   Los complementos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Los complementos son archivos DLL que implementan dos tipos de compatibilidad con Windows PowerShell para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   Un conjunto de cmdlets de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los cmdlets son comandos que implementan una acción concreta. Por ejemplo, **Invoke-Sqlcmd** ejecuta un script de [!INCLUDE[tsql](../../includes/tsql-md.md)] o XQuery que también se puede ejecutar mediante la utilidad **sqlcmd** e **Invoke-PolicyEvaluation** notifica si los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cumplen las directivas de administración basada en directivas.  
  
    -   Un proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El proveedor permite navegar por la jerarquía de objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando una ruta de acceso similar a una ruta de acceso al sistema de archivos. Cada objeto se asocia a una clase de los modelos de objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Puede utilizar los métodos y las propiedades de la clase para realizar un trabajo en los objetos. Por ejemplo, si cambia el directorio a un objeto de bases de datos en una ruta de acceso, puede utilizar los métodos y las propiedades de la clase Microsoft.SqlServer.Managment.SMO.Database para administrar la base de datos.  
  
-   El **sqlps** módulo que se importa en las sesiones de Windows PowerShell 2.0 para cargar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] complementos.  
  
-   El desuso **sqlps** utilidad que inicia una sesión de Windows PowerShell 2.0 e importa el **sqlps** módulo.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] admite el inicio de sesiones de Windows PowerShell desde el árbol del Explorador de objetos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es compatible con los pasos de trabajo de Windows PowerShell.  
  
 Si no ha instalado Windows PowerShell 2.0, o se ha desinstalado, debe instalarlo siguiendo las instrucciones de la [Windows Management Framework](http://go.microsoft.com/fwlink/?LinkId=186214) página.  
  
 Si se desinstala Windows PowerShell una vez finalizada la instalación, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las características de Windows PowerShell no funcionarán. Los usuarios de Windows pueden desinstalar Windows PowerShell y puede ser necesario desinstalar Windows PowerShell para realizar determinadas actualizaciones del sistema operativo Windows. Para usar las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell, debe volver a instalar PowerShell 2.0 utilizando Windows Management Framework.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  
  
  
