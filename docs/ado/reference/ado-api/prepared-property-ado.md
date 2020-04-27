---
title: Propiedad Prepared (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Prepared
helpviewer_keywords:
- Prepared property [ADO]
ms.assetid: 11ca8825-765e-4bb4-a6ce-3f6564ad8755
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee7a94a06aa574c84c01cb8b9d05ebfcdf327d44
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917594"
---
# <a name="prepared-property-ado"></a>Propiedad Prepared (ADO)
Indica si se debe guardar una versión compilada de un [comando](../../../ado/reference/ado-api/command-object-ado.md) antes de la ejecución.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor **booleano** que, si se establece en **true**, indica que el comando debe estar preparado.  
  
## <a name="remarks"></a>Observaciones  
 Use la propiedad **Prepared** para que el proveedor guarde una versión preparada (o compilada) de la consulta especificada en la propiedad [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) antes de la primera ejecución de un objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) . Esto puede ralentizar la primera ejecución de un comando, pero una vez que el proveedor compila un comando, el proveedor usará la versión compilada del comando para las ejecuciones posteriores, lo que dará como resultado un rendimiento mejorado.  
  
 Si la propiedad es **false**, el proveedor ejecutará el objeto de **comando** directamente sin crear una versión compilada.  
  
 Si el proveedor no admite la preparación de comandos, puede devolver un error si esta propiedad se establece en **true**. Si el proveedor no devuelve un error, simplemente omite la solicitud para preparar el comando y establece la propiedad **preparado** en **false**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad Prepared (VB)](../../../ado/reference/ado-api/prepared-property-example-vb.md)   
 [Ejemplo de la propiedad Prepared (VC ++)](../../../ado/reference/ado-api/prepared-property-example-vc.md)   
