---
title: Propiedad DefaultDatabase | Documentos de Microsoft
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
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b7fc72d99273428a1ab4a11f12a021079d8faac
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277464"
---
# <a name="defaultdatabase-property"></a>Propiedad DefaultDatabase
Indica la base de datos predeterminada para un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor que se evalúa como el nombre de una base de datos disponible desde el proveedor.  
  
## <a name="remarks"></a>Notas  
 Use la **DefaultDatabase** propiedad para establecer o devolver el nombre de la base de datos predeterminada en un determinado **conexión** objeto.  
  
 Si hay una base de datos de forma predeterminada, las cadenas de SQL pueden usar una sintaxis incompleta para tener acceso a objetos en esa base de datos. Para obtener acceso a objetos en una base de datos distinto del especificado en el **DefaultDatabase** propiedad, debe calificar nombres de objeto con el nombre de la base de datos deseada. Tras establecer la conexión, el proveedor escribirá información de base de datos predeterminada para el **DefaultDatabase** propiedad. Algunos proveedores permiten sólo una base de datos por conexión, en cuyo caso no se puede cambiar la **DefaultDatabase** propiedad.  
  
 Algunos orígenes de datos y los proveedores pueden no admitir esta característica y pueden devolver un error o una cadena vacía.  
  
> [!NOTE]
>  **Uso de servicios de datos remoto** esta propiedad no está disponible en un cliente **conexión** objeto.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo Provider y DefaultDatabase propiedades (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Ejemplo de las propiedades Provider y DefaultDatabase (VC ++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   
