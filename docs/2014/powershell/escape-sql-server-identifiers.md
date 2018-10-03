---
title: Identificadores de SQL Server de escape | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1df587280d7dbf42e22c7f472a792e6f401c79fd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48073795"
---
# <a name="escape-sql-server-identifiers"></a>Identificadores de SQL Server de escape
  A menudo, se puede usar el carácter de escape de acento invertido (`) de Windows PowerShell para hacer que se eludan los caracteres que se permiten en los identificadores delimitados de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pero no en los nombres de ruta de Windows PowerShell. Sin embargo, algunos caracteres no se pueden evitar. Por ejemplo, no puede hacer que se eluda el carácter de dos puntos (:) en Windows PowerShell. Los identificadores con ese carácter deben codificarse. La codificación es más confiable que hacer que el carácter se eluda porque funciona para todos los caracteres.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
 El carácter de acento invertido (`) suele estar en la tecla de la parte superior izquierda del teclado, debajo de la tecla ESC.  
  
## <a name="examples"></a>Ejemplos  
 Este es un ejemplo en el que se hace que se eluda un carácter #:  
  
```  
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```  
  
 Este es un ejemplo en el que se hace que se eluda un paréntesis al especificar (local) como nombre de equipo:  
  
```  
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```  
  
## <a name="see-also"></a>Vea también  
 [Identificadores de SQL Server en PowerShell](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
