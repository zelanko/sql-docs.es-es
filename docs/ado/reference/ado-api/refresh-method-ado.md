---
title: "Actualizar (método, ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords:
- Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 422f04618e6e63b6143a8459c869316e47450796
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="refresh-method-ado"></a>Actualizar (método, ADO)
Actualiza los objetos de una colección para reflejar los objetos disponibles y específicos del proveedor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>Comentarios  
 El **actualizar** método realiza diferentes tareas según la colección desde el que se llame al método.  
  
### <a name="parameters"></a>Parámetros  
 Mediante el **actualizar** método en el [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) colección de un [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto recupera información de parámetro del proveedor para el procedimiento almacenado o consulta parametrizada especificados en el **comando** objeto. La colección estará vacía para los proveedores que no admiten llamadas a procedimientos almacenados o consultas parametrizadas.  
  
 Debe establecer el [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad de la **comando** objeto válido [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto, el [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propiedad en un comando válido y el [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) propiedad **adCmdStoredProc** antes de llamar a la **actualizar** método.  
  
 Si tiene acceso a la **parámetros** colección antes de llamar a la **actualizar** método, ADO automáticamente se llame al método y rellenar la colección.  
  
> [!NOTE]
>  Si usas el **actualizar** método para obtener información sobre los parámetros desde el proveedor y devuelve uno o más tipos de datos de longitud variable [parámetro](../../../ado/reference/ado-api/parameter-object.md) objetos, ADO puede asignar memoria para los parámetros de acuerdo en su tamaño máximo potencial, lo que provocará un error durante la ejecución. Debe establecerse explícitamente la [tamaño](../../../ado/reference/ado-api/size-property-ado-parameter.md) propiedad para estos parámetros antes de llamar a la [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método para evitar errores.  
  
### <a name="fields"></a>Campos  
 Mediante el **actualizar** método en el [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección no tiene ningún efecto visible. Para recuperar los cambios de la estructura de base de datos subyacente, debe utilizar el [Requery](../../../ado/reference/ado-api/requery-method.md) método o, si la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto no admite marcadores, el [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)(método).  
  
### <a name="properties"></a>Propiedades  
 Mediante el **actualizar** método en un **propiedades** colección de algunos objetos rellena la colección con las propiedades dinámicas que expone el proveedor. Estas propiedades proporcionan información sobre la funcionalidad específica del proveedor, más allá de las propiedades integradas ADO admite.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Colección Axes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Colección de columnas](../../../ado/reference/adox-api/columns-collection-adox.md)|[Colección CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Colección de dimensiones](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Colección de errores](../../../ado/reference/ado-api/errors-collection-ado.md)|[Fields (colección)](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Colección de grupos](../../../ado/reference/adox-api/groups-collection-adox.md)|[Colección Hierarchies](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Colección de índices](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Colección de claves](../../../ado/reference/adox-api/keys-collection-adox.md)|[Colección de niveles](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Colección de miembros](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Colección de parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Colección de posiciones](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Colección de procedimientos](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Colección de propiedades](../../../ado/reference/ado-api/properties-collection-ado.md)|[Colección de tablas](../../../ado/reference/adox-api/tables-collection-adox.md)|[Colección de usuarios](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Colección de vistas](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Vea también  
 [Actualización de ejemplo del método (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Actualización de ejemplo del método (VC ++)](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Count (propiedad, ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
