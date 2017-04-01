---
title: "Cmdlet New-RestoreLocation | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 5ca13d8c-1c5d-4f02-869c-72e0defce6d7
caps.latest.revision: 11
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 11
---
# Cmdlet New-RestoreLocation
  Especifica la información utilizada para restaurar una base de datos.  
  
## Sintaxis  
 `New-RestoreLocation [-File <String>] [-DataSourceId <String>] [-ConnectionString <String>] [-DataSourceType <RestoreDataSourceType>] [-Folders <RestoreFolder[]>] [-AsTemplate] [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 `New-RestoreLocation [-Server <String>] [-Credential <PSCredential>] [-Verbose] [-Debug] [-ErrorAction <ActionPreference>] [-WarningAction <ActionPreference>] [-ErrorVariable <String>] [-WarningVariable <String>] [-OutVariable <String>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]`  
  
 Los parámetros comunes, como –Verbose, -Debug, parámetros de error y advertencia, -Whatif y –Confirm, se incluyen en la referencia de Windows PowerShell. Para obtener más información, vea [about_Commonparameters](http://technet.microsoft.com/library/dd315352.aspx).  
  
## Description  
 El cmdlet New-RestoreLocation contiene información utilizada para restaurar una base de datos, incluida la cadena de conexión del servidor y la base de datos, las propiedades del origen de datos, los archivos y las carpetas asociadas a la base de datos que se restaura.  
  
## Parámetros  
  
### -File \<cadena>  
 Especifica el nombre del archivo de copia de seguridad que se está restaurando.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -DataSourceId \<cadena>  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -ConnectionString \<cadena>  
 Especifica la cadena de conexión de una instancia de Analysis Services remota.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -DataSourceType \<AS.RestoreDataSourceType>  
 Especifica si el origen de datos es remoto o local, en función de la ubicación de la partición.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -Folders \<AS.RestoreFolder>  
 Especifica las carpetas de partición en el equipo local o la instancia remota.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -AsTemplate \<SwitchParameter>  
 Especifica si el objeto se debe crear en la memoria y devolver.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -Server \<cadena>  
 Especifica la instancia de Analysis Services a la que el cmdlet se conectará y ejecutará. Si no se proporciona un nombre de servidor, se establecerá una conexión al host local. Para las instancias predeterminadas, especifique solo el nombre del servidor. Para las instancias con nombre, utilice el formato nombreDeServidor\nombreDeInstancia. En las conexiones HTTP, utilice el formato http[s]://server[:port]/virtualdirectory/msmdpump.dll.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|localhost|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -Credential \<PSCredential>  
 Este parámetro se utiliza para pasar un nombre de usuario y una contraseña cuando se utiliza una conexión HTTP a una instancia de Analysis Services, para una instancia que ha configurado para el acceso HTTP. Para obtener más información, vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md) y [Scripting de PowerShell en Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md) para conexiones HTTP.  
  
 Si se especifica este parámetro, el nombre de usuario y la contraseña se utilizarán para conectarse a la instancia de Analysis Server especificada. Si no se especifica ninguna credencial, se utilizará la cuenta predeterminada de Windows del usuario que ejecuta la herramienta.  
  
 Para usar este parámetro, cree primero un objeto PSCredential con Get-Credential para especificar el nombre de usuario y la contraseña (por ejemplo, `$Cred=Get-Credential “adventure-works\bobh”`. Después, puede canalizar este objeto al parámetro –Credential `(-Credential:$Cred`).  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|True (ByValue)|  
|¿Aceptar caracteres comodín?|false|  
  
## Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|None|  
|Salidas|None|  
  
## Ejemplos  
  
## Vea también  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [Administrar modelos tabulares con PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  