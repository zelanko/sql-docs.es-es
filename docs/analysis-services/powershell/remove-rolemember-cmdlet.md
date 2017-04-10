---
title: "Cmdlet Remove-RoleMember | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: e38f56ab-facd-4bef-9502-f52f8486a6a6
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 8
---
# Cmdlet Remove-RoleMember
  Quitar un miembro del rol especificado de una base de datos de Analysis Services.  
  
## Sintaxis  
 `Remove-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Remove-RoleMember [-DatabaseRole] <Microsoft.AnalysisServices.Role> [-MemberName] <System.String>  [<CommonParameters>]`  
  
## Description  
 El cmdlet Remove-RoleMember quita un miembro existente de un rol de una base de datos de Analysis Services.  
  
## Parámetros  
  
### -MemberName \<string>  
 Especifica el usuario o grupo de Windows que se va a quitar del rol.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -Database \<string>  
 Especifica la base de datos a la que el rol pertenece.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|1|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -RoleName \<string>  
 Especifica el rol del que va a quitar miembros.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|2|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -DatabaseRole \<string>  
 Especifica el objeto Microsoft.AnalysisServices.Role del que se está quitando el miembro. Utilice este parámetro como alternativa a los parámetros –Database y –RoleName, si desea proporcionar el rol de base de datos a través de una canalización.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true (ByPropertyName)|  
|¿Aceptar caracteres comodín?|false|  
  
### \<CommonParameters>  
 Este cmdlet admite los parámetros comunes: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer y -OutVariable. Para obtener más información, vea [about_Commonparameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Entradas y salidas  
 Ninguno.  
  
## Ejemplo 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 Este comando quita una cuenta de usuario de dominio de Windows del rol Lector, para la base de datos AdventureWorks que se ejecuta en una instancia predeterminada local.  
  
## Ejemplo 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 La línea 1 agrega todos los roles de base de datos de la base de datos AWTEST a la canalización. La línea 2, donde escribe $roles en el símbolo del sistema, muestra la matriz de roles. La línea 3 quita el usuario “adventure-works\bobh” de Windows del primer rol en la matriz.  
  
## Ejemplo 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Remove-rolemember –membername “adventure-works\bobh”  
```  
  
 Este comando quita una cuenta de usuario de dominio de Windows del primer rol en una matriz, donde la matriz se crea enumerando los elementos secundarios de la carpeta Roles, en el contexto de una base de datos específica (AWTEST).  
  
## Vea también  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [Administrar modelos tabulares con PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  