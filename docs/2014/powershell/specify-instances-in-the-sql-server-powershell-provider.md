---
title: Especificar instancias del proveedor de PowerShell de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 9373de68-fd43-45f2-b9a6-149c96610aeb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 414d9135989c39ea183d14d2d6f5dfa6e84e6fe6
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797757"
---
# <a name="specify-instances-in-the-sql-server-powershell-provider"></a>Especificar instancias del proveedor de PowerShell de SQL Server
  Las rutas de acceso especificadas para el proveedor de PowerShell de SQL Server deben identificar la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] y el equipo en que se está ejecutando. La sintaxis para especificar el equipo y la instancia debe cumplir las reglas de los identificadores de SQL Server y las rutas de acceso de Windows PowerShell.  
  
1.  **Antes de empezar:**  [Limitaciones y restricciones](#LimitationsRestrictions)  
  
2.  **Para especificar una instancia:**  [Ejemplos](#Examples)  
  
## <a name="before-you-begin"></a>Antes de comenzar  
 El primer nodo situado a continuación de SQLSERVER:\SQL en una ruta de acceso de proveedor de SQL Server es el nombre del equipo en el que se ejecuta la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)], por ejemplo:  
  
```  
SQLSERVER:\SQL\MyComputer  
```  
  
 Si está ejecutando Windows PowerShell en el mismo equipo que la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)], puede usar localhost o (local) en lugar del nombre del equipo. Los scripts que usan localhost o (local) se pueden ejecutar en cualquier equipo sin tener que cambiar para reflejar los distintos nombres de los equipos.  
  
 Puede ejecutar varias instancias del programa ejecutable de [!INCLUDE[ssDE](../includes/ssde-md.md)] en el mismo equipo. El nodo situado a continuación del nombre del equipo en una ruta de acceso del proveedor de SQL Server identifica la instancia; por ejemplo:  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance  
```  
  
 Cada equipo puede tener una instancia predeterminada de [!INCLUDE[ssDE](../includes/ssde-md.md)]. No especifique un nombre para la instancia predeterminada al instalarla. Si especifica solamente un nombre de equipo en una cadena de conexión, se conectará a la instancia predeterminada en ese equipo. Todas las demás instancias en el equipo deben ser instancias con nombre. Durante la instalación se especifica el nombre de instancia y las cadenas de conexión deben especificar tanto el nombre de equipo como el nombre de instancia.  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 No puede usar un punto (.) para especificar el equipo local en los scripts de PowerShell. No se admite el punto porque PowerShell lo interpreta como comando.  
  
 Windows PowerShell suele tratar como comandos los caracteres que van entre paréntesis de (local). Debe codificarlos o convertirlos para poderlos usar en una ruta de acceso, o agregar la ruta de acceso entre comillas dobles. Para obtener más información, vea Codificar y descodificar identificadores de SQL Server.  
  
 El proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] requiere que siempre se especifique un nombre de instancia. Para las instancias predeterminadas, debe especificar el nombre de instancia DEFAULT.  
  
##  <a name="Examples"></a> Ejemplos; Equipo y nombres de instancia  
 En este ejemplo se usan el host local y DEFAULT para especificar la instancia predeterminada en el equipo local:  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT
```  
  
 Windows PowerShell suele tratar como comandos los caracteres que van entre paréntesis de (local). Debe:  
  
-   Poner las cadenas de ruta de acceso entre comillas:  
  
    ```powershell
    Set-Location "SQLSERVER:\SQL\(local)\DEFAULT"  
    ```  
  
-   Eludir el paréntesis mediante el carácter de acento invertido (`).  
  
    ```powershell
    Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
    ```  
  
-   Codificar el paréntesis mediante su representación hexadecimal:  
  
    ```powershell
    Set-Location SQLSERVER:\SQL\%28local%29\DEFAULT  
    ```  
  
## <a name="see-also"></a>Ver también  
 [Identificadores de SQL Server en PowerShell](sql-server-identifiers-in-powershell.md)   
 [Proveedor de PowerShell de SQL Server](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
