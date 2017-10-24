---
title: Cmdlet Add-RoleMember | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 827c8bbc-d48f-4e49-9ea5-abb1380f7623
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e2a71e5b4fb5aae12ce16b419da832d4b1237d28
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="add-rolemember-cmdlet"></a>Cmdlet Add-RoleMember

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Agrega un miembro al rol especificado de una base de datos multidimensional o tabular de Analysis Services.  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
## <a name="syntax"></a>Sintaxis  
 `Add-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Add-RoleMember [-MemberName] <System.String> [-DatabaseRole] <Microsoft.AnalysisServices.Role> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 El cmdlet Add-RoleMember agrega un miembro válido a un rol de base de datos existente. Solo se permiten los roles de base de datos. No puede utilizar este cmdlet para agregar miembros a un rol de servidor.  
  
 Puede agregar solo un miembro a la vez, que puede ser un usuario o cuenta de grupo.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-membername-string"></a>-MemberName \<cadena >  
 Especifica el usuario o grupo de Windows que se van a agregar al rol.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-database-string"></a>-Base de datos \<cadena >  
 Especifica la base de datos a la que el rol pertenece.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|1|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-rolename-string"></a>-RoleName \<cadena >  
 Especifica el rol al que está agregando los miembros.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|2|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-databaserole-string"></a>-DatabaseRole \<cadena >  
 Especifica el objeto Microsoft.AnalysisServices.Role al que el miembro se va a agregar. Utilice este parámetro como alternativa a los parámetros –Database y –RoleName, si desea proporcionar el rol de base de datos a través de una canalización.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true (ByPropertyName)|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet admite los parámetros comunes: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer y -OutVariable. Para más información, vea [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|Ninguno.|  
|Salidas|None|  
  
## <a name="example-1"></a>Ejemplo 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 Este comando agrega una cuenta de usuario de dominio de Windows al rol de Lector, para la base de datos AdventureWorks que se ejecuta en una instancia predeterminada local.  
  
## <a name="example-2"></a>Ejemplo 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 La línea 1 agrega todos los roles de base de datos de la base de datos AWTEST a la canalización. La línea 2, donde escribe $roles en el símbolo del sistema, muestra la matriz de roles. La línea 3 agrega el usuario adventure-works\bobh de Windows como miembro del primer rol en la matriz.  
  
## <a name="example-3"></a>Ejemplo 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Add-rolemember –membername “adventure-works\bobh”  
```  
  
 Este comando agrega una cuenta de usuario de dominio de Windows al rol en una matriz, donde la matriz se crea enumerando los elementos secundarios de la carpeta Roles, en el contexto de una base de datos específica (AWTEST).  
  

  
  

