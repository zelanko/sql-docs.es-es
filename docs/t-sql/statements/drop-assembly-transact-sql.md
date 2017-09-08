---
title: DROP ASSEMBLY (Transact-SQL) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP ASSEMBLY
- DROP_ASSEMBLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- deleting assemblies
- assemblies [CLR integration], removing
- dropping assemblies
- WITH NO DEPENDENTS option
ms.assetid: 452d181a-a8e6-44a3-975d-29966d01b18d
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c38654a3ce90b4e1605cfdbe1db7a49ddac8b6b1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="drop-assembly-transact-sql"></a>DROP ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un ensamblado y todos sus archivos asociados de la base de datos actual. Los ensamblados se crean mediante el uso de [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md) y modificar mediante [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
DROP ASSEMBLY [ IF EXISTS ] assembly_name [ ,...n ]  
[ WITH NO DEPENDENTS ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *IF EXISTE*  
 **Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Condicionalmente quita el ensamblado solo si ya existe.  
  
 *ASSEMBLY_NAME*  
 Es el nombre del ensamblado que desea quitar.  
  
 WITH NO DEPENDENTS  
 Si se especifica, solo quita *assembly_name* y ninguno de los ensamblados dependientes que hace referencia el ensamblado. Si no se especifica, DROP ASSEMBLY quita *assembly_name* y todos los ensamblados dependientes.  
  
## <a name="remarks"></a>Comentarios  
 Al quitar un ensamblado se quita el propio ensamblado y todos sus archivos asociados, como el código de origen y los archivos de depuración, de la base de datos.  
  
 Si no se especifica WITH NO DEPENDENTS, DROP ASSEMBLY quita *assembly_name* y todos los ensamblados dependientes. Si se generan errores al intentar quitar los ensamblados dependientes, DROP ASSEMBLY devuelve un error.  
  
 DROP ASSEMBLY devuelve un error si otro ensamblado que existe en la base de datos hace referencia al ensamblado o si se utiliza en procedimientos, desencadenadores, tipos definidos por el usuario, agregados o funciones de CLR (Common Language Runtime) en la base de datos actual.  
  
 DROP ASSEMBLY no interfiere con el código al que se hace referencia en el ensamblado que se ejecuta actualmente. No obstante, después de ejecutar DROP ASSEMBLY, los intentos de llamar el código de ensamblado generarán errores.  
  
## <a name="permissions"></a>Permissions  
 Se requiere la propiedad del ensamblado o permiso CONTROL en él.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se asume que el ensamblado `HelloWorld` ya está creado en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
DROP ASSEMBLY Helloworld ;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREAR ENSAMBLADOS &#40; Transact-SQL &#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [ALTER ASSEMBLY &#40; Transact-SQL &#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Obtener información acerca de los ensamblados](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  

