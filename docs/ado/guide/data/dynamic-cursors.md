---
title: Los cursores dinámicos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], dynamic
- dynamic cursors [ADO]
ms.assetid: 00460f30-8cf7-494e-82df-41012f40ae51
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0d7a19476a00fb88e0b2195c761993f91b7a5d4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838333"
---
# <a name="dynamic-cursors"></a>Cursores dinámicos
Los cursores dinámicos detectan todos los cambios realizados en las filas del conjunto de resultados, independientemente de si se producen los cambios desde dentro del cursor o por otros usuarios fuera del cursor. Todos los insert, update y las instrucciones delete realizadas por todos los usuarios son visibles a través del cursor. El cursor dinámico puede detectar los cambios realizados en las filas, orden y los valores del conjunto de resultados una vez abierto el cursor. Las actualizaciones realizadas fuera del cursor no son visibles hasta que se confirman (a menos que el nivel de aislamiento de transacción de cursor se establece en "no confirmado").  
  
 Por ejemplo, suponga que un cursor dinámico recupera dos filas y otra aplicación y, a continuación, actualiza una de esas filas y elimina la otra. Si el cursor dinámico, a continuación, captura las filas, no encontrará la fila eliminada, pero mostrará los nuevos valores de la fila actualizada.  
  
 El cursor dinámico es una buena opción si la aplicación debe detectar todas las actualizaciones simultáneas realizadas por otros usuarios. Utilice la **adOpenDynamic CursorTypeEnum** para indicar que desea utilizar un cursor dinámico en ADO.  
  
## <a name="see-also"></a>Vea también  
 [Cursores de solo avance](../../../ado/guide/data/forward-only-cursors.md)   
 [Cursores estáticos](../../../ado/guide/data/static-cursors.md)   
 [Cursores KEYSET](../../../ado/guide/data/keyset-cursors.md)
