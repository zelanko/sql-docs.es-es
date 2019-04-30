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
ms.openlocfilehash: b25921a7b48ecd818527dd95ebc2d8714cb6871d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187056"
---
# <a name="sqlps-utility"></a>sqlps, utilidad
  La utilidad `sqlps` inicia una sesión de Windows PowerShell 2.0 con el proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell y los cmdlets cargados y registrados. Puede escribir scripts o comandos de PowerShell que usen los componentes de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell para trabajar con instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y sus objetos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)] En su lugar, use el módulo `sqlps` de PowerShell. Para obtener más información sobre la `sqlps` módulo, consulte [importar el módulo SQLPS](../database-engine/import-the-sqlps-module.md).  
  
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
 Especifica que el `sqlps` salida de la utilidad formatearse como cadenas de texto (**texto**) o en un formato CLIXML serializado (**XML**).  
  
 **-InPutFormat** { **Text** | **XML** }  
 Especifica que la entrada para el `sqlps` utilidad se da formato como cadenas de texto (**texto**) o en un formato CLIXML serializado (**XML**).  
  
 **-Command**  
 Especifica el comando que debe ejecutar la utilidad `sqlps`. El `sqlps` utilidad ejecuta el comando y, a continuación, se cierra, a menos que **- NoExit** también se especifica. No especifique ningún otro modificador después de **-Command**; se leerían como parámetros del comando.  
  
 **-**  
 **-Command -** especifica que el `sqlps` utilidad lee la entrada desde la entrada estándar.  
  
 *script_block* [ **-args**_argument_array_ ]  
 Especifica un bloque de comandos de PowerShell que se han de ejecutar; el bloque debe incluirse entre llaves: {}. *Script_block* solo se puede especificar cuando el `sqlps` utilidad se llama desde **PowerShell** u otro `sqlps` sesión de la utilidad. *argument_array* es una matriz de variables de PowerShell que contiene los argumentos de los comandos de PowerShell en *script_block*.  
  
 *string* [ *command_parameters* ]  
 Especifica una cadena que contiene los comandos de PowerShell que se han de ejecutar. Use el formato **"& {*`command`*}"**. Las comillas indican una cadena y el operador de invocación (&) hace que el `sqlps` utilidad para ejecutar el comando.  
  
 [ **-?** | **-Help** ]  
 Muestra el resumen de la sintaxis de las opciones de la utilidad `sqlps`.  
  
## <a name="remarks"></a>Comentarios  
 El `sqlps` utilidad inicia el entorno de PowerShell (PowerShell.exe) y carga el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] módulo de PowerShell. El módulo, también denominado `sqlps`, carga y registra estos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] complementos de PowerShell:  
  
-   Microsoft.SqlServer.Management.PSProvider.dll  
  
     Implementa el proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell y cmdlets asociados como **Encode-SqlName** y **Decode-SqlName**.  
  
-   Microsoft.SqlServer.Management.PSSnapin.dll  
  
     Implementa los cmdlets **Invoke-Sqlcmd** e **Invoke-PolicyEvaluation** .  
  
 Puede usar la utilidad `sqlps` para realizar las tareas siguientes:  
  
-   Ejecutar interactivamente comandos de PowerShell.  
  
-   Ejecutar archivos de script de PowerShell.  
  
-   Ejecutar cmdlets de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Usar las rutas de acceso del proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para navegar por la jerarquía de objetos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 De forma predeterminada, el `sqlps` utilidad se ejecuta con la directiva de ejecución de scripting establecida en **Restricted**. Esto evita la ejecución de cualquier script de PowerShell. Puede usar el cmdlet **Set-ExecutionPolicy** para habilitar la ejecución de scripts firmados o de cualquier script. Ejecute solo scripts de orígenes de confianza y proteja todos los archivos de entrada y salida con los permisos NTFS adecuados. Para obtener más información sobre cómo habilitar los scripts de PowerShell, vea [Running Windows PowerShell Scripts](https://www.tech-recipes.com/rx/2513/powershell_enable_script_support/).  
  
 La versión de la utilidad `sqlps` en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] y en [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] se implementó como un shell mínimo de Windows PowerShell 1.0. Los shells mínimos tienen ciertas restricciones, como no permitir que los usuarios carguen complementos distintos de los que ha cargado el shell mínimo. Estas restricciones no se aplican a la versión [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] y posteriores de la utilidad, que se han cambiado para usar el módulo `sqlps`.  
  
## <a name="examples"></a>Ejemplos  
 **A. Ejecutar la utilidad sqlps en modo predeterminado e interactivo sin el título de copyright**  
  
```  
sqlps -NoLogo  
```  
  
 **B. Ejecutar un script de SQL Server PowerShell desde el símbolo del sistema**  
  
```  
sqlps -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
 **C. Ejecutar un script de SQL Server PowerShell desde el símbolo del sistema y continuar la ejecución una vez que el script se complete**  
  
```  
sqlps -NoExit -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
## <a name="see-also"></a>Vea también  
 [Habilitar o deshabilitar un protocolo de red de servidor](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
