---
title: Comando exclusivo | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a5ab2ccf22c7322fa0e35cd281a8953b7685a02
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
