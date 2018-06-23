---
title: Identificadores de SQL Server de escape | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
caps.latest.revision: 6
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: b11d666165c266467fbdbe46a5d95fb8d7dbad70
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106988"
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
  
  