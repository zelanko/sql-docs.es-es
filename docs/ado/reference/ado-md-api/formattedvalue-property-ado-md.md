---
description: FormattedValue (propiedad, ADO MD)
title: Propiedad FormattedValue (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell::FormattedValue
- FormattedValue
helpviewer_keywords:
- FormattedValue property [ADO MD]
ms.assetid: 5c06451e-06ec-4da6-9a87-2d043469248a
author: rothja
ms.author: jroth
ms.openlocfilehash: 5905b4aba040505c60fa78721718b3ab03c51622
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986706"
---
# <a name="formattedvalue-property-ado-md"></a>FormattedValue (propiedad, ADO MD)
Indica la presentación con formato de un valor de [celda](./cell-object-ado-md.md) .  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve una **cadena** y es de solo lectura.  
  
## <a name="remarks"></a>Observaciones  
 Use la propiedad **FormattedValue** para obtener el valor de presentación con formato de la propiedad [Value](./value-property-ado-md.md) de un objeto [Cell](./cell-object-ado-md.md) . Por ejemplo, si el valor de una celda era 1056,87 y este valor representa una cantidad de dólar, **FormattedValue** sería $1.056,87.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Cell (ADO MD)](./cell-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de Cellset (VB)](./cellset-example-vb.md)   
 [Value (propiedad) (ADO MD)](./value-property-ado-md.md)