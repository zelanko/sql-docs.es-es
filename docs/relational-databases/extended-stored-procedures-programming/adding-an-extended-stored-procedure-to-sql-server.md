---
title: Agregar un total procedimiento almacenado a SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], adding
- adding extended stored procedures
- collations [SQL Server], extended stored procedures
ms.assetid: 10f1bb74-3b43-4efd-b7ab-7a85a8600a50
caps.latest.revision: 39
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 44d3315e58a0aecd77219952a45bf77385350626
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="adding-an-extended-stored-procedure-to-sql-server"></a>Agregar un procedimiento almacenado extendido a SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 Un archivo DLL que contiene funciones de procedimiento almacenado extendido actúa como extensión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar el archivo DLL, copie el archivo en un directorio, como la carpeta que contenga el estándar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] archivos DLL (C:\Program Files\Microsoft SQL Server\MSSQL12.0. *x*\MSSQL\Binn de forma predeterminada).  
  
 Una vez que haya copiado en el servidor el archivo DLL de procedimiento almacenado extendido, un administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe registrar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cada una de las funciones de procedimiento almacenado extendido del archivo DLL. Para ello, debe utilizarse el procedimiento almacenado del sistema sp_addextendedproc.  
  
> [!IMPORTANT]  
>  Antes de agregar el procedimiento almacenado extendido al servidor y otorgar permisos de ejecución a otros usuarios, el administrador del sistema debe revisarlo por completo para asegurarse de que no contenga código perjudicial o malintencionado.  Valide todos los datos proporcionados por el usuario. No concatene ninguna entrada de usuario antes de validarla. No ejecute nunca un comando creado a partir de una entrada de usuario no validada.  
  
 El primer parámetro de sp_addextendedproc especifica el nombre de la función y el segundo parámetro especifica el nombre del archivo DLL donde reside dicha función. Se recomienda especificar la ruta de acceso completa del archivo DLL.  
  
> [!IMPORTANT]  
>  Los archivos DLL existentes que no se hayan registrado con una ruta de acceso completa no funcionarán tras una actualización a SQL Server 2005 o posterior. Para corregir el problema, utilice sp_dropextendedproc con el fin de eliminar el archivo DLL del registro y, a continuación, vuelva a registrarlo con sp_addextendedproc, especificando la ruta de acceso completa.  
  
 El nombre de la función especificada en `sp_addextendedproc` debe ser exactamente el mismo que el nombre de la función del archivo DLL, incluidas las mayúsculas y minúsculas. Por ejemplo, este comando registra una función `xp_hello,` situada en un archivo dll denominado `xp_hello.dll`, como un procedimiento almacenado extendido de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_addextendedproc 'xp_hello', 'c:\Program Files\Microsoft SQL Server\MSSQL13.0.MSSQLSERVER\MSSQL\Binn\xp_hello.dll';  
```  
  
 Si el nombre de la función especificada en `sp_addextendedproc` no coincide exactamente con el nombre de función del archivo DLL, el nuevo nombre se registrará en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero no podrá utilizarse. Por ejemplo, aunque `xp_Hello` está registrado como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ubicado en procedimiento almacenado extendido `xp_hello.dll`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá encontrar la función en el archivo DLL si usa `xp_Hello` para llamar posteriormente a la función.  
  
```  
--Register the function (xp_hello) with an initial upper case  
sp_addextendedproc 'xp_Hello', 'c:\xp_hello.dll';  
  
--Use the newly registered name to call the function  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
--This is the error message  
Server: Msg 17750, Level 16, State 1, Procedure xp_Hello, Line 1  
Could not load the DLL xp_hello.dll, or one of the DLLs it references. Reason: 127(The specified procedure could not be found.).  
```  
  
 Si el nombre de la función especificada en `sp_addextendedproc` coincide exactamente con el nombre de función del archivo DLL y la intercalación de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no distingue mayúsculas de minúsculas, el usuario puede llamar al procedimiento almacenado extendido utilizando cualquier combinación de letras mayúsculas y minúsculas en el nombre.  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will succeed in calling xp_hello  
DECLARE @txt varchar(33);  
EXEC xp_Hello @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HelLO @txt OUTPUT;  
  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
```  
  
 Cuando la intercalación de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] distinga mayúsculas de minúsculas, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá llamar al procedimiento almacenado extendido (aunque se haya registrado exactamente con el mismo nombre e intercalación que la función del archivo DLL) si se llama al procedimiento con distintas letras mayúsculas y minúsculas.  
  
```  
--Register the function (xp_hello)  
sp_addextendedproc 'xp_hello', 'c:\xp_hello.dll';  
  
--The following will result in an error  
DECLARE @txt varchar(33);  
EXEC xp_HELLO @txt OUTPUT;  
  
--This is the error  
Server: Msg 2812, Level 16, State 62, Line 1  
```  
  
 No es necesario detener y reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
