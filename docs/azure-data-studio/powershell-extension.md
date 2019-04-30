---
title: Extensión de PowerShell
titleSuffix: Azure Data Studio
description: Instalar y usar PowerShell para Azure Data Studio
ms.custom: seodec18
ms.date: 04/19/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: matthend
ms.openlocfilehash: 0ffb46d5d498ba04a6916e7e2d56ffccaaa71aef
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63137171"
---
# <a name="powershell-editor-support-for-azure-data-studio"></a>Compatibilidad con el Editor para Studio datos de Azure PowerShell

Esta extensión ofrece compatibilidad enriquecida del editor de PowerShell en [Azure Data Studio](https://github.com/Microsoft/azuredatastudio).
Ahora puede escribir y depurar scripts de PowerShell mediante la interfaz excelente similar a IDE que proporciona Studio de datos de Azure.

![Extensión de PowerShell](media/powershell-extension/powershell-extension.png)


## <a name="features"></a>Características

- Resaltado de sintaxis
- Fragmentos de código
- IntelliSense para los cmdlets y mucho más
- Análisis basado en reglas que proporciona [PowerShell Script Analyzer](http://github.com/PowerShell/PSScriptAnalyzer)
- Ir a definición de los cmdlets y las variables
- Buscar las referencias de cmdlets y las variables
- Detección de símbolos de documento y el área de trabajo
- Ejecutar selección seleccionado del uso de código de PowerShell <kbd>F8</kbd>
- Iniciar la Ayuda en línea para el símbolo bajo el cursor mediante <kbd>Ctrl</kbd>+<kbd>F1</kbd>
- Soporte técnico básico consola interactiva.


## <a name="installing-the-extension"></a>Instalar la extensión

Puede instalar la versión oficial de la extensión de PowerShell siguiendo los pasos descritos en la [documentación de Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/extensions).
En el panel de extensiones, busque "PowerShell" extensión y su instalación.  ¡Obtener le notificará automáticamente sobre cualquier actualización futura extensión!

También puede instalar un paquete VSIX desde nuestro [página versiones](https://github.com/PowerShell/vscode-powershell/releases) e instalarlo a través de la línea de comandos:

```powershell
azuredatastudio --install-extension PowerShell-<version>.vsix
```

## <a name="platform-support"></a>Compatibilidad con plataformas

- **Windows 7 a 10** con Windows PowerShell v3 y versiones posteriores y PowerShell Core
- **Linux** con PowerShell Core (todas las distribuciones compatibles de PowerShell)
- **macOS** con PowerShell Core

Leer el [preguntas más frecuentes sobre](https://github.com/PowerShell/vscode-powershell/wiki/FAQ) para obtener respuestas a preguntas habituales.

## <a name="installing-powershell-core"></a>Instalación de PowerShell Core

Si usa Azure Data Studio en Mac OS o Linux, también es posible que deba instalar PowerShell Core.

PowerShell Core es un proyecto de código abierto en [GitHub](https://github.com/powershell/powershell).
Para obtener más información acerca de cómo instalar PowerShell Core en plataformas MacOS o Linux, consulte los artículos siguientes:

- [Instalación de PowerShell Core en Linux](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [Instalación de PowerShell Core en macOS](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)

## <a name="example-scripts"></a>Scripts de ejemplo

Hay algunas secuencias de comandos de ejemplo en la extensión `examples` carpeta que puede usar para detectar la edición y depuración de la funcionalidad de PowerShell.  Consulte las [README.md](https://github.com/PowerShell/vscode-powershell/blob/master/examples/README.md) archivo para obtener más información sobre cómo usarlas.

Esta carpeta se encuentra en la siguiente ruta:

```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.PowerShell-<version>/examples
```

o si usa la versión preliminar de la extensión

 ```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.powershell-preview-<version>/examples
```

Para abrir/ver ejemplos de la extensión en Azure Data Studio, ejecute lo siguiente desde el símbolo del sistema de PowerShell:

```powershell
azuredatastudio (Get-ChildItem $Home\.azuredatastudio\extensions\ms-vscode.PowerShell-*\examples)[-1]
```

### <a name="sql-powershell-examples"></a>Ejemplos de PowerShell SQL
Para poder usar estos ejemplos (abajo), deberá instalar el módulo SqlServer desde el [Galería de PowerShell](https://www.powershellgallery.com/packages/SqlServer).

```powershell
Install-Module -Name SqlServer
```

> [!NOTE]
> Con la versión `21.1.18102` y superiores, el `SqlServer` módulo admite [PowerShell Core](https://github.com/PowerShell/PowerShell) 6.2 y, además de Windows PowerShell.

En este ejemplo, usamos el `Get-SqlInstance` para obtener los objetos de SMO Server para servidora y ServidorB.  El valor predeterminado para este comando incluirá el nombre de instancia de salida versión Service Pack & nivel de actualización de CU de las instancias.

```powershell
Get-SqlInstance -ServerInstance ServerA, ServerB
```

Este es un ejemplo de lo que el resultado será como:

```
Instance Name             Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------             -------    ------------ -----------  ------------ ----------------
ServerA                   13.0.5233  SP2          CU4          Windows      Windows Server 2016 Datacenter
ServerB                   14.0.3045  RTM          CU12         Linux        Ubuntu
```

En el ejemplo siguiente, se realizará una `dir` (alias de `Get-ChildItem`) para obtener la lista de todas las instancias de SQL Server aparece en el archivo de servidores registrados y, a continuación, utilice el `Get-SqlDatabase` para obtener una lista de bases de datos para cada una de esas instancias.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE { $_.Mode -ne 'd' } |
FOREACH {
    Get-SqlDatabase -ServerInstance $_.Name
}
```

Este es un ejemplo de lo que el resultado será como:

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa
master               Normal        6.00 MB  368.00 KB Simple       140 sa
model                Normal       16.00 MB    5.53 MB Full         140 sa
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa
```

Este ejemplo se usa el `Get-SqlDatabase` cmdlet para recuperar una lista de todas las bases de datos en la instancia del servidor b, a continuación, presenta una cuadrícula o una tabla (mediante la `Out-GridView` cmdlet) para seleccionar qué bases de datos realizar copias de seguridad.  Una vez que el usuario hace clic en el botón "Aceptar", solo las bases de datos resaltadas se realizará una copia.

```powershell
Get-SqlDatabase -ServerInstance ServerB |
Out-GridView -PassThru |
Backup-SqlDatabase -CompressionOption On
```

En este ejemplo, una vez más, obtiene las listas de todas las instancias de SQL Server aparece en el archivo de servidores registrados, a continuación, llama a la `Get-SqlAgentJobHistory` que informa de cada trabajo del Agente SQL con errores desde la medianoche, para cada instancia de SQL Server que se muestran.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE {$_.Mode -ne 'd' } |
FOREACH {
    Get-SqlAgentJobHistory -ServerInstance  $_.Name -Since Midnight -OutcomesType Failed
}
```

### <a name="sql-powershell-examples"></a>Ejemplos de PowerShell SQL
Para poder usar estos ejemplos (abajo), deberá instalar el módulo SqlServer desde el [Galería de PowerShell](https://www.powershellgallery.com/packages/SqlServer).

```powershell
Install-Module -Name SqlServer -AllowPrerelease
```

En este ejemplo, usamos el `Get-SqlInstance` para obtener los objetos de SMO Server para servidora y ServidorB.  El valor predeterminado para este comando incluirá el nombre de instancia de salida versión Service Pack & nivel de actualización de CU de las instancias.

```powershell
Get-SqlInstance -ServerInstance ServerA, ServerB
```

Este es un ejemplo de lo que el resultado será como:

```
Instance Name             Version    ProductLevel UpdateLevel
-------------             -------    ------------ -----------
ServerA                   13.0.5233  SP2          CU4
ServerB                   14.0.3045  RTM          CU12
```

En este ejemplo, se realizará una `dir` (alias de `Get-ChildItem`) para obtener la lista de todas las instancias de SQL Server aparece en el archivo de servidores registrados y, a continuación, utilice el `Get-SqlDatabase` para obtener una lista de bases de datos para cada una de esas instancias.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE { $_.Mode -ne 'd' } |
FOREACH {
    Get-SqlDatabase -ServerInstance $_.Name
}
```

Este es un ejemplo de lo que el resultado será como:

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level      
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa   
master               Normal        6.00 MB  368.00 KB Simple       140 sa   
model                Normal       16.00 MB    5.53 MB Full         140 sa   
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa   
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa   
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa   
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa   
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa   
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa   
```

Este ejemplo se usa el `Get-SqlDatabase` cmdlet para recuperar una lista de todas las bases de datos en la instancia del servidor b, a continuación, presenta una cuadrícula o una tabla (mediante la `Out-GridView` cmdlet) para seleccionar qué bases de datos realizar copias de seguridad.  Una vez que el usuario hace clic en el botón "Aceptar", solo las bases de datos resaltadas se realizará una copia.

```powershell
Get-SqlDatabase -ServerInstance ServerB |
Out-GridView -PassThru |
Backup-SqlDatabase -CompressionOption On
```

En este ejemplo, una vez más, obtiene una lista de todas las instancias de SQL Server aparece en el archivo de servidores registrados, a continuación, llama a la `Get-SqlAgentJobHistory` que informa de cada trabajo del Agente SQL con errores desde la medianoche, para cada instancia de SQL Server que se muestran.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE {$_.Mode -ne 'd' } |
FOREACH {
    Get-SqlAgentJobHistory -ServerInstance  $_.Name -Since Midnight -OutcomesType Failed
}
```

## <a name="reporting-problems"></a>Problemas de informes

Si experimenta algún problema con la extensión de PowerShell, consulte [los documentos de solución de problemas](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md) para obtener información sobre el diagnóstico de problemas e informes.

#### <a name="security-note"></a>Nota de seguridad

Problemas de seguridad, consulte [aquí](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md#note-on-security).

## <a name="contributing-to-the-code"></a>Contribución al código

Consulte la [documentación de desarrollo](https://github.com/PowerShell/vscode-powershell/blob/master/docs/development.md) para obtener más información sobre cómo contribuir a esta extensión.

## <a name="maintainers"></a>Mantenedores de

- [Keith Hill](https://github.com/rkeithhill) - [@r_keith_hill](http://twitter.com/r_keith_hill)
- [Tyler Leonhardt](https://github.com/tylerl0706) - [@TylerLeonhardt](http://twitter.com/tylerleonhardt)
- [Rob Holt](https://github.com/rjmholt)

## <a name="license"></a>Licencia

Esta extensión es [con licencia bajo la licencia MIT](https://github.com/PowerShell/vscode-powershell/blob/master/LICENSE.txt). Para obtener más información sobre los archivos binarios de terceros que se incluyen con las versiones de este proyecto, vea el [avisos de terceros](https://github.com/PowerShell/vscode-powershell/blob/master/Third%20Party%20Notices.txt) archivo.

## <a name="code-of-conductconduct-md"></a>[Código de conducta][conduct-md]

Este proyecto se ha adoptado el [Microsoft código de conducta de código abierto][conduct-code].
Para obtener más información, consulte el [código de conducta preguntas más frecuentes sobre] [ conduct-FAQ] o póngase en contacto con [ opencode@microsoft.com ] [ conduct-email] con otras preguntas o comentarios.

[conduct-code]: http://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: http://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[conduct-md]: https://github.com/PowerShell/vscode-powershell/blob/master/CODE_OF_CONDUCT.md
