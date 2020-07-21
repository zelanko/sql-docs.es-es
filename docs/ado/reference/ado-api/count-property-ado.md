---
title: Propiedad Count (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Count
helpviewer_keywords:
- Count property [ADO]
ms.assetid: da9ccd1f-d402-41a2-940c-45556fc5340d
author: rothja
ms.author: jroth
ms.openlocfilehash: 9b611546b63dec8484785ba855f299925933e89e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760241"
---
# <a name="count-property-ado"></a>Count (propiedad, ADO)
Indica el número de objetos de una colección.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor **Long** .  
  
## <a name="remarks"></a>Comentarios  
 Utilice la propiedad **Count** para determinar el número de objetos que hay en una colección determinada.  
  
 Dado que la numeración de los miembros de una colección comienza con cero, siempre debe codificar los bucles empezando por el miembro cero y terminando con el valor de la propiedad **Count** menos 1. Si usa Microsoft Visual Basic y desea crear un bucle a través de los miembros de una colección sin comprobar la propiedad Count, utilice el **parámetro** **for each... Comando siguiente** .  
  
 Si la propiedad **Count** es cero, no hay ningún objeto en la colección.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Colección Axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Colección de columnas (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Colección CubeDefs (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Colección Dimensions (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Colección de errores (ADO)](../../../ado/reference/ado-api/errors-collection-ado.md)|[Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Colección de grupos (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Colección Hierarchies (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Colección de índices (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Colección de claves (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Colección de niveles (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Colección Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Colección de parámetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Colección de posiciones (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Colección de procedimientos (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)|[Colección de tablas (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|[Colección de usuarios (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Colección de vistas (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad Count (VB)](../../../ado/reference/ado-api/count-property-example-vb.md)   
 [Ejemplo de la propiedad Count (VC + +)](../../../ado/reference/ado-api/count-property-example-vc.md)   
 [Actualizar (método, ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
