---
description: FormattedValue (propiedad, ADO MD)
title: Propiedad FormattedValue (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: ba8b3469d017b79027670cb4de9f8b3761c8dcc7
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778134"
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