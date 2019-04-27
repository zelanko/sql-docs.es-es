---
title: Instalar SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a90a30a0ae7fe09d49b1d42b577b13370c48c0de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775445"
---
# <a name="install-sql-server-powershell"></a>Instalar SQL Server PowerShell
  El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se detendrá si detecta que existen características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seleccionadas que incluyen componentes de PowerShell, pero no está instalado Windows PowerShell 2.0. Debe instalar PowerShell utilizando Windows Management Framework y, a continuación, volver a ejecutar el programa de instalación.  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-powershell-support"></a>Instalar compatibilidad con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell  
 Debe instalar el software que proporciona compatibilidad con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Windows PowerShell utilizando el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando selecciona características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que requieren compatibilidad con PowerShell, el programa de instalación comprueba si Windows PowerShell 2.0 está instalado. Si PowerShell 2.0 está presente, el programa de instalación instala los siguientes componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell:  
  
-   Los complementos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Los complementos son archivos DLL que implementan dos tipos de compatibilidad con Windows PowerShell para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   Un conjunto de cmdlets de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los cmdlets son comandos que implementan una acción concreta. Por ejemplo, **Invoke-Sqlcmd** ejecuta un script de [!INCLUDE[tsql](../../includes/tsql-md.md)] o XQuery que también se puede ejecutar mediante la utilidad **sqlcmd** e **Invoke-PolicyEvaluation** notifica si los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cumplen las directivas de administración basada en directivas.  
  
    -   Un proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El proveedor permite navegar por la jerarquía de objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando una ruta de acceso similar a una ruta de acceso al sistema de archivos. Cada objeto se asocia a una clase de los modelos de objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Puede utilizar los métodos y las propiedades de la clase para realizar un trabajo en los objetos. Por ejemplo, si cambia el directorio a un objeto de bases de datos en una ruta de acceso, puede utilizar los métodos y las propiedades de la clase Microsoft.SqlServer.Managment.SMO.Database para administrar la base de datos.  
  
-   El **sqlps** módulo que se importa en las sesiones de Windows PowerShell 2.0 para cargar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] complementos.  
  
-   El desuso **sqlps** utilidad que inicia una sesión de Windows PowerShell 2.0 e importa el **sqlps** módulo.  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] admite el inicio de sesiones de Windows PowerShell desde el árbol del Explorador de objetos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es compatible con los pasos de trabajo de Windows PowerShell.  
  
 Si no ha instalado Windows PowerShell 2.0, o se ha desinstalado, debe instalarlo siguiendo las instrucciones de la [Windows Management Framework](https://go.microsoft.com/fwlink/?LinkId=186214) página.  
  
 Si se desinstala Windows PowerShell después de finalizar la instalación, las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Windows PowerShell no funcionarán. Los usuarios de Windows pueden desinstalar Windows PowerShell y puede ser necesario desinstalar Windows PowerShell para realizar determinadas actualizaciones del sistema operativo Windows. Para usar las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell, debe volver a instalar PowerShell 2.0 utilizando Windows Management Framework.  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  
  
  
