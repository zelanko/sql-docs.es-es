---
title: Comando EXCLUSIVO ESTABLECIDO (SET EXCLUSIVE Command) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXCLUSIVE command [ODBC]
ms.assetid: d4fe12c5-7e8b-4d20-9ea4-2bcaffb271f2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d140c4be3ab850547ac82f9b954e7313b008dbf0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300865"
---
# <a name="set-exclusive-command"></a>Comando exclusivo de Set
Especifica si los archivos de tabla se abren para uso exclusivo o compartido en una red.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET EXCLUSIVE ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ACTIVAR  
 Limita la accesibilidad de una tabla abierta en una red al usuario que la abrió. Otros usuarios de la red no pueden acceder a la tabla. SET EXCLUSIVE ON también evita que todos los demás usuarios tengan acceso de solo lectura.  
  
 Apagado  
 (Predeterminado para el controlador; los valores predeterminados para Visual FoxPro son ON para la sesión de datos global y OFF para una sesión de datos privadas.) Permite que cualquier usuario de la red comparta y modifique una tabla abierta en una red.  
  
## <a name="remarks"></a>Observaciones  
 Cambiar la configuración de SET EXCLUSIVE no cambia el estado de las tablas abiertas anteriormente. Por ejemplo, si se abre una tabla con SET EXCLUSIVE establecido en ON y SET EXCLUSIVE se cambia posteriormente a OFF, la tabla conserva su estado de uso exclusivo.  
  
## <a name="see-also"></a>Consulte también  
 [Cuadro de diálogo de configuración de Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)
