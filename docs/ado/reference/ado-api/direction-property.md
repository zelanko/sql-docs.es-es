---
title: Propiedad Direction | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Direction
helpviewer_keywords:
- Direction property
ms.assetid: d5732578-3434-4dcd-a9f7-db1abd1b3b94
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab3eecc4e1d4ec0f14634d9c5ce77375f7432231
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277904"
---
# <a name="direction-property"></a>Propiedad Direction
Indica si la [parámetro](../../../ado/reference/ado-api/parameter-object.md) representa un parámetro de entrada, un parámetro de salida, una entrada y un parámetro de salida, o si el parámetro es el valor devuelto de un procedimiento almacenado.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [ParameterDirectionEnum](../../../ado/reference/ado-api/parameterdirectionenum.md) valor.  
  
## <a name="remarks"></a>Notas  
 Use la **dirección** propiedad para especificar cómo se pasa un parámetro a o desde un procedimiento. El **dirección** propiedad es de lectura/escritura, lo que permite trabajar con proveedores que no devuelven dicha información o para definir esta información cuando no desea que ADO realice una llamada adicional al proveedor para recuperar información de parámetros.  
  
 No todos los proveedores pueden determinar la dirección de parámetros en sus procedimientos almacenados. En estos casos, debe establecer el **dirección** propiedad antes de ejecutar la consulta.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)  
  
## <a name="see-also"></a>Vea también  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VC ++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
