---
description: Cursores dinámicos
title: Cursores dinámicos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], dynamic
- dynamic cursors [ADO]
ms.assetid: 00460f30-8cf7-494e-82df-41012f40ae51
author: rothja
ms.author: jroth
ms.openlocfilehash: e8ce85233cec96af3d804652225b4d14698287db
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991356"
---
# <a name="dynamic-cursors"></a>Cursores dinámicos
Los cursores dinámicos detectan todos los cambios realizados en las filas del conjunto de resultados, independientemente de si los cambios se producen dentro del cursor o por otros usuarios fuera del cursor. Todas las instrucciones INSERT, Update y DELETE realizadas por todos los usuarios son visibles a través del cursor. El cursor dinámico puede detectar los cambios realizados en las filas, el orden y los valores del conjunto de resultados después de abrir el cursor. Las actualizaciones realizadas fuera del cursor no son visibles hasta que se confirman (a menos que el nivel de aislamiento de transacción del cursor se establezca en "uncommited").  
  
 Por ejemplo, supongamos que un cursor dinámico captura dos filas y otra aplicación y, a continuación, actualiza una de esas filas y elimina la otra. Si después el cursor dinámico captura esas filas, no encontrará la que se ha eliminado, pero mostrará los valores nuevos para la fila actualizada.  
  
 El cursor dinámico es una buena opción si la aplicación debe detectar todas las actualizaciones simultáneas realizadas por otros usuarios. Use el **AdOpenDynamic CursorTypeEnum** para indicar que desea utilizar un cursor dinámico en ADO.  
  
## <a name="see-also"></a>Consulte también  
 [Cursores de solo avance](./forward-only-cursors.md)   
 [Cursores estáticos](./static-cursors.md)   
 [Cursores KEYSET](./keyset-cursors.md)