---
title: Cmdlet Remove-RoleMember | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eec431908e2159f7021613c086f1278cb2954b43
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="remove-rolemember-cmdlet"></a>Cmdlet Remove-RoleMember
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Quitar un miembro del rol especificado de una base de datos de Analysis Services.  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
## <a name="syntax"></a>Sintaxis  
 `Remove-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Remove-RoleMember [-DatabaseRole] <Microsoft.AnalysisServices.Role> [-MemberName] <System.String>  [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 El cmdlet Remove-RoleMember quita un miembro existente de un rol de una base de datos de Analysis Services.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-membername-string"></a>-MemberName \<cadena >  
 Especifica el usuario o grupo de Windows que se va a quitar del rol.  
  
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
 Especifica el rol del que va a quitar miembros.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|2|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-databaserole-string"></a>-DatabaseRole \<cadena >  
 Especifica el objeto Microsoft.AnalysisServices.Role del que se está quitando el miembro. Utilice este parámetro como alternativa a los parámetros –Database y –RoleName, si desea proporcionar el rol de base de datos a través de una canalización.  
  
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
 Ninguno.  
  
## <a name="example-1"></a>Ejemplo 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 Este comando quita una cuenta de usuario de dominio de Windows del rol Lector, para la base de datos AdventureWorks que se ejecuta en una instancia predeterminada local.  
  
## <a name="example-2"></a>Ejemplo 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 La línea 1 agrega todos los roles de base de datos de la base de datos AWTEST a la canalización. La línea 2, donde escribe $roles en el símbolo del sistema, muestra la matriz de roles. La línea 3 quita el usuario “adventure-works\bobh” de Windows del primer rol en la matriz.  
  
## <a name="example-3"></a>Ejemplo 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Remove-rolemember –membername “adventure-works\bobh”  
```  
  
 Este comando quita una cuenta de usuario de dominio de Windows del primer rol en una matriz, donde la matriz se crea enumerando los elementos secundarios de la carpeta Roles, en el contexto de una base de datos específica (AWTEST).  
  

  
  
