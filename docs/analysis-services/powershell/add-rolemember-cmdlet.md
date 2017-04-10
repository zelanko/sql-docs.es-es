---
title: "Cmdlet Add-RoleMember | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 827c8bbc-d48f-4e49-9ea5-abb1380f7623
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 14
---
# Cmdlet Add-RoleMember
  Agrega un miembro al rol especificado de una base de datos multidimensional o tabular de Analysis Services.  
  
## Sintaxis  
 `Add-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Add-RoleMember [-MemberName] <System.String> [-DatabaseRole] <Microsoft.AnalysisServices.Role> [<CommonParameters>]`  
  
## Description  
 El cmdlet Add-RoleMember agrega un miembro válido a un rol de base de datos existente. Solo se permiten los roles de base de datos. No puede utilizar este cmdlet para agregar miembros a un rol de servidor.  
  
 Puede agregar solo un miembro a la vez, que puede ser un usuario o cuenta de grupo.  
  
## Parámetros  
  
### -MemberName \<string>  
 Especifica el usuario o grupo de Windows que se van a agregar al rol.  
  
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
 Especifica el rol al que está agregando los miembros.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|2|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -DatabaseRole \<string>  
 Especifica el objeto Microsoft.AnalysisServices.Role al que el miembro se va a agregar. Utilice este parámetro como alternativa a los parámetros –Database y –RoleName, si desea proporcionar el rol de base de datos a través de una canalización.  
  
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
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|Ninguno.|  
|Salidas|None|  
  
## Ejemplo 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 Este comando agrega una cuenta de usuario de dominio de Windows al rol de Lector, para la base de datos AdventureWorks que se ejecuta en una instancia predeterminada local.  
  
## Ejemplo 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 La línea 1 agrega todos los roles de base de datos de la base de datos AWTEST a la canalización. La línea 2, donde escribe $roles en el símbolo del sistema, muestra la matriz de roles. La línea 3 agrega el usuario adventure-works\bobh de Windows como miembro del primer rol en la matriz.  
  
## Ejemplo 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Add-rolemember –membername “adventure-works\bobh”  
```  
  
 Este comando agrega una cuenta de usuario de dominio de Windows al rol en una matriz, donde la matriz se crea enumerando los elementos secundarios de la carpeta Roles, en el contexto de una base de datos específica (AWTEST).  
  
## Vea también  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [Administrar modelos tabulares con PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  