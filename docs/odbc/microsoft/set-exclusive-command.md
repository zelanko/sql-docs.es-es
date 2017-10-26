---
title: Comando exclusivo | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 830cec1dbb87ae2bc4336d28d6112fd76b4db0ed
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="set-exclusive-command"></a>Comando exclusivo de Set.
Especifica si los archivos de la tabla se abren para su uso exclusivo o compartido en una red.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Accesibilidad de los límites de una tabla que se abren en una red para el usuario que abrió. La tabla no es accesible para otros usuarios de la red. SET exclusivo ON también impide que los demás usuarios que tengan acceso de solo lectura.  
  
 OFF  
 (Valor predeterminado para el controlador; los valores predeterminados de Visual FoxPro son ON para la sesión de datos globales y OFF para una sesión de datos privados). Permite que una tabla que se abren en una red para compartirse y modificadas por cualquier usuario de la red.  
  
## <a name="remarks"></a>Comentarios  
 Cambiar la configuración de establecer exclusivo no cambia el estado de las tablas abiertas previamente. Por ejemplo, si se abre una tabla con establecer exclusivo establecida en ON y establecer exclusivo posteriormente se cambia a OFF, la tabla conserva su estado de uso exclusivo.  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo de configuración de Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)

