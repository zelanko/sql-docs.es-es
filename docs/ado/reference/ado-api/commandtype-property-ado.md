---
title: La propiedad CommandType (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandType
helpviewer_keywords:
- CommandType property [ADO]
ms.assetid: ca44809c-8647-48b6-a7fb-0be70a02f53e
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2008231e7daba12fbbabf81ce5e0e6b79b41cd80
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="commandtype-property-ado"></a>Propiedad CommandType (ADO)
Indica el tipo de un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve uno o varios [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valores.  
  
> [!NOTE]
>  No utilice la **CommandTypeEnum** valores de **adCmdFile** o **adCmdTableDirect** con **CommandType**. Estos valores sólo pueden utilizarse como opciones con el [abiertos](../../../ado/reference/ado-api/open-method-ado-recordset.md) y [Requery](../../../ado/reference/ado-api/requery-method.md) métodos de un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="remarks"></a>Comentarios  
 Use la **CommandType** propiedad para optimizar la evaluación de la [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad.  
  
 Si el **CommandType** valor de la propiedad se establece en el valor predeterminado, **adCmdUnknown**, puede experimentar una disminución del rendimiento porque ADO debe realizar llamadas al proveedor para determinar si el  **CommandText** propiedad es una instrucción SQL, un procedimiento almacenado o un nombre de tabla. Si sabe qué tipo de comando que está utilizando, al establecer el **CommandType** propiedad indica a ADO que vaya directamente al código pertinente. Si el **CommandType** propiedad no coincide con el tipo de comando en el **CommandText** propiedad, se produce un error al llamar a la [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (VC ++)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamaño y ejemplo de propiedades de dirección (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
