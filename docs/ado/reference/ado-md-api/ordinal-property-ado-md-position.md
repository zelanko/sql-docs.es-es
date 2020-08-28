---
description: Propiedad ordinal (posición de ADO MD)
title: Propiedad ordinal (posición ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Position::Ordinal
- Ordinal
helpviewer_keywords:
- Ordinal property [ADO MD]
ms.assetid: 6efe8b5d-a2d5-43a9-a5ea-f9244f8d4ec9
author: rothja
ms.author: jroth
ms.openlocfilehash: 6d2485e8331a3eee95cfd5937ffbdbd570b2ecdc
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986196"
---
# <a name="ordinal-property-ado-md-position"></a>Propiedad ordinal (posición de ADO MD)
Identifica de forma única una [posición](./position-object-ado-md.md) a lo largo de un eje.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un entero **largo** y es de solo lectura.  
  
## <a name="remarks"></a>Observaciones  
 La propiedad **ordinal** de un objeto de [posición](./position-object-ado-md.md) corresponde al índice de la **posición** dentro de la colección de [posiciones](./positions-collection-ado-md.md) .  
  
 Una celda se puede recuperar rápidamente utilizando el **ordinal** de la **posición** a lo largo de cada eje con la propiedad [Item](./item-property-ado-md-cellset.md) del objeto [Cellset](./cellset-object-ado-md.md) .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Position (ADO MD)](./position-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Objeto Cellset (ADO MD)](./cellset-object-ado-md.md)   
 [Propiedad Item (ADO MD Cellset)](./item-property-ado-md-cellset.md)   
 [Propiedad ordinal (celda de ADO MD)](./ordinal-property-ado-md-cell.md)