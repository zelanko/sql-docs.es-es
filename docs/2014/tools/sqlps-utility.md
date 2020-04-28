---
title: sqlps, utilidad | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqlps utility
- PowerShell [SQL Server], sqlps utility
ms.assetid: 4b2515a6-12c3-44fb-b263-1c567681cd2b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ff96b99ee7982be89126e79687dbc8a2215f42f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72798135"
---
# <a name="sqlps-utility"></a>sqlps, utilidad
  La utilidad `sqlps` inicia una sesión de Windows PowerShell 2.0 con el proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell y los cmdlets cargados y registrados. Puede escribir scripts o comandos de PowerShell que usen los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell para trabajar con instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y sus objetos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)] En su lugar, use el módulo `sqlps` de PowerShell. Para obtener más información sobre `sqlps` el módulo, consulte [importar el módulo SQLPS](../database-engine/import-the-sqlps-module.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      sqlps   
[ [ [ -NoLogo ][ -NoExit ][ -NoProfile ]  
    [ -OutPutFormat { Text | XML } ] [ -InPutFormat { Text | XML } ]  
  ]  
  [ -Command { -  
             | script_block [ -argsargument_array ]  
             | string [ command_parameters ]  
             }  
  ]  
]  
[ -? | -Help ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-NoLogo**  
 Especifica que la utilidad `sqlps` debe ocultar el título de copyright cuando se inicia.  
  
 **-NoExit**  
 Especifica que la utilidad `sqlps` debe seguir ejecutándose después de que los comandos de inicio se hayan completado.  
  
 **-NoProfile**  
 Especifica que la utilidad `sqlps` no debe cargar un perfil de usuario. Los perfiles de usuario registran los alias, funciones y variables de uso frecuente para usarlos en las sesiones de PowerShell.  
  
 **-OutPutFormat** { **Text** | **XML** }  
 Especifica que se `sqlps` dé formato a la salida de la utilidad como cadenas de texto (**Text**) o en un formato CLIXML serializado (**XML**).  
  
 **-InPutFormat** { **Text** | **XML** }  
 Especifica que se dé formato `sqlps` a la entrada de la utilidad como cadenas de texto (**Text**) o en un formato CLIXML serializado (**XML**).  
  
 **-Command**  
 Especifica el comando que debe ejecutar la utilidad `sqlps`. La `sqlps` utilidad ejecuta el comando y, a continuación, se cierra, a menos que también se especifique **-NoExit** . No especifique ningún otro modificador después de **-Command**; se leerían como parámetros del comando.  
  
 **-**  
 **-Command:** especifica que la `sqlps` utilidad lee la entrada de la entrada estándar.  
  
 *script_block* [ **-args**_argument_array_ ]  
 Especifica un bloque de comandos de PowerShell que se han de ejecutar; el bloque debe incluirse entre llaves: {}. *Script_block* solo se puede especificar cuando se `sqlps` llama a la utilidad desde **PowerShell** o desde `sqlps` otra sesión de la utilidad. *argument_array* es una matriz de variables de PowerShell que contiene los argumentos de los comandos de PowerShell en *script_block*.  
  
 *string* [ *command_parameters* ]  
 Especifica una cadena que contiene los comandos de PowerShell que se han de ejecutar. Use el formato **"& {*`command`*}"**. Las comillas indican una cadena y el operador de invocación (&) hace `sqlps` que la utilidad ejecute el comando.  
  
 [ **-?** |  **-Help** ]  
 Muestra el resumen de la sintaxis de las opciones de la utilidad `sqlps`.  
  
## <a name="remarks"></a>Observaciones  
 La `sqlps` utilidad inicia el entorno de PowerShell (PowerShell. exe) y carga [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] el módulo de PowerShell. El módulo, también denominado `sqlps`, carga y registra estos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] complementos de PowerShell:  
  
-   Microsoft.SqlServer.Management.PSProvider.dll  
  
     Implementa el proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell y cmdlets asociados como **Encode-SqlName** y **Decode-SqlName**.  
  
-   Microsoft.SqlServer.Management.PSSnapin.dll  
  
     Implementa los cmdlets **Invoke-Sqlcmd** e **Invoke-PolicyEvaluation** .  
  
 Puede usar la utilidad `sqlps` para realizar las tareas siguientes:  
  
-   Ejecutar interactivamente comandos de PowerShell.  
  
-   Ejecutar archivos de script de PowerShell.  
  
-   Ejecutar cmdlets de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Usar las rutas de acceso del proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para navegar por la jerarquía de objetos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 De forma predeterminada, `sqlps` la utilidad se ejecuta con la Directiva de ejecución de scripting establecida en **Restricted**. Esto evita la ejecución de cualquier script de PowerShell. Puede usar el cmdlet **Set-ExecutionPolicy** para habilitar la ejecución de scripts firmados o de cualquier script. Ejecute solo scripts de orígenes de confianza y proteja todos los archivos de entrada y salida con los permisos NTFS adecuados. Para obtener más información sobre cómo habilitar los scripts de PowerShell, vea [Running Windows PowerShell Scripts](https://www.tech-recipes.com/rx/2513/powershell_enable_script_support/).  
  
 La versión de la utilidad `sqlps` en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] y en [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] se implementó como un shell mínimo de Windows PowerShell 1.0. Los shells mínimos tienen ciertas restricciones, como no permitir que los usuarios carguen complementos distintos de los que ha cargado el shell mínimo. Estas restricciones no se aplican a la versión [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] y posteriores de la utilidad, que se han cambiado para usar el módulo `sqlps`.  
  
## <a name="examples"></a>Ejemplos  

### <a name="a-run-the-sqlps-utility-in-default-interactive-mode-without-the-copyright-banner"></a>A. Ejecutar la utilidad sqlps en modo predeterminado e interactivo sin el título de copyright
  
```cmd
sqlps -NoLogo  
```  
  
### <a name="b-run-a-sql-server-powershell-script-from-the-command-prompt"></a>B. Ejecutar un script de SQL Server PowerShell desde el símbolo del sistema
  
```cmd
sqlps -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
### <a name="c-run-a-sql-server-powershell-script-from-the-command-prompt-and-keep-running-after-the-script-completes"></a>C. Ejecutar un script de SQL Server PowerShell desde el símbolo del sistema y continuar la ejecución una vez que el script se complete
  
```cmd
sqlps -NoExit -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
## <a name="see-also"></a>Consulte también  
 [Habilitar o deshabilitar un protocolo de red de servidor](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
