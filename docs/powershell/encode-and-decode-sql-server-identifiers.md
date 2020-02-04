---
title: Codificar y descodificar identificadores de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 21e642feba6a2726aa4d5615f6ae508fa33c1694
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67934652"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>Codificar y descodificar identificadores de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Los identificadores delimitados de SQL Server a veces contienen caracteres no admitidos en las rutas de acceso de Windows PowerShell. Estos caracteres se pueden especificar codificando sus valores hexadecimales.  

> [!NOTE]
> Hay dos módulos de SQL Server PowerShell: **SqlServer** y **SQLPS**. El módulo **SQLPS** está incluido en la instalación de SQL Server (por motivos de compatibilidad con versiones anteriores), pero ya no se actualiza. El módulo de PowerShell más actualizado es **SqlServer**. El módulo **SqlServer** contiene versiones actualizadas de los cmdlets en **SQLPS**, así como nuevos cmdlets para admitir las características más recientes de SQL.  
> Las versiones anteriores del módulo **SqlServer***estaban incluidas* en SQL Server Management Studio (SSMS), pero solo con las versiones 16.x de SSMS. Para usar PowerShell con SSMS 17.0 y versiones posteriores, debe tener el módulo **SqlServer** instalado desde la Galería de PowerShell.
> Para instalar el módulo **SqlServer**, consulte [Instalar SQL Server PowerShell](download-sql-server-ps-module.md).
  
  
Los caracteres que no se permiten en los nombres de ruta de Windows PowerShell se pueden representar, o codificar, como el carácter "%" seguido del valor hexadecimal del modelo de bits que representa el carácter, como en " **%** xx". La codificación siempre se puede usar para controlar los caracteres que no se admiten en las rutas de Windows PowerShell.  
  
 El cmdlet **Encode-SqlName** toma como entrada un identificador de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Genera una cadena con todos los caracteres que no son admitidos por el lenguaje de Windows PowerShell codificados con "%xx". El cmdlet **Decode-SqlName** toma como entrada un identificador de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] codificado y devuelve el identificador original.  
  
##  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 Los cmdlets **Encode-Sqlname** y **Decode-Sqlname** solo codifican o descodifican caracteres que se permiten en los identificadores delimitados de SQL Server, pero no solo se admiten en las rutas de PowerShell. Estos son los caracteres codificados por **Encode-SqlName** y descodificados por **Decode-SqlName**:  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**Carácter**|\ |/|:|%|\<|>|*|?|[|]|&#124;|  
|**Codificación hexadecimal**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="EncodeIdent"></a> Codificar un identificador  
 **Para codificar un identificador de SQL Server en una ruta de acceso de PowerShell**  
  
-   Use uno de los dos métodos para codificar un identificador de SQL Server:  
  
    -   Especifique el código hexadecimal para el carácter no compatible mediante la sintaxis %XX, donde el código hexadecimal es XX.  
  
    -   Transfiera el identificador como una cadena entrecomillada al cmdlet **Encode-Sqlname** .  
  
### <a name="examples-encoding"></a>Ejemplos (codificación)  
 Este ejemplo especifica la versión codificada del carácter (%3A) ":":  
  
```  
Set-Location Table%3ATest  
```  
  
 También puede usar **Encode-SqlName** para compilar un nombre admitido por Windows PowerShell:  
  
```  
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="DecodeIdent"></a> Descodificar un identificador  
 **Descodificar un identificador de SQL Server de una ruta de PowerShell**  
  
 Use el cmdlet **Decode-Sqlname** para reemplazar las codificaciones hexadecimales por caracteres representados por la codificación.  
  
### <a name="examples-decoding"></a>Ejemplos (descodificación)  
 Este ejemplo devuelve “Table:Test”:  
  
```  
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>Consulte también  
 [Identificadores de SQL Server en PowerShell](sql-server-identifiers-in-powershell.md)   
 [Proveedor de PowerShell de SQL Server](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
