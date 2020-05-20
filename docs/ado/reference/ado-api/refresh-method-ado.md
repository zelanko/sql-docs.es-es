---
title: Refresh (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Collection::Refresh
- Parameters::Refresh
- Properties::Refresh
helpviewer_keywords:
- Refresh method [ADO]
ms.assetid: 089b7ca7-684f-4259-8032-5bd1ecc54426
author: rothja
ms.author: jroth
ms.openlocfilehash: 48fc3a1adf8dbeae010e4035ac4f2e390c015e54
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82756535"
---
# <a name="refresh-method-ado"></a>Actualizar (método, ADO)
Actualiza los objetos de una colección para reflejar los objetos disponibles en el proveedor y específicos de este.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
collection.Refresh  
```  
  
## <a name="remarks"></a>Comentarios  
 El método **Refresh** realiza diferentes tareas en función de la colección de la que se llama.  
  
### <a name="parameters"></a>Parámetros  
 El uso del método **Refresh** en la colección [Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md) de un objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) recupera información de parámetros del proveedor para el procedimiento almacenado o la consulta con parámetros especificados en el objeto **Command** . La colección estará vacía para los proveedores que no admitan llamadas a procedimientos almacenados o consultas parametrizadas.  
  
 Debe establecer la propiedad [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) del objeto de **comando** en un objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) válido, la propiedad [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) en un comando válido y la propiedad [CommandType](../../../ado/reference/ado-api/commandtype-property-ado.md) en **adCmdStoredProc** antes de llamar al método **Refresh** .  
  
 Si obtiene acceso a la colección **Parameters** antes de llamar al método **Refresh** , ADO llamará automáticamente al método y rellenará la colección.  
  
> [!NOTE]
>  Si usa el método **Refresh** para obtener información de parámetros del proveedor y devuelve uno o más objetos de [parámetro](../../../ado/reference/ado-api/parameter-object.md) de tipo de datos de longitud variable, ADO puede asignar memoria para los parámetros en función de su tamaño máximo potencial, lo que producirá un error durante la ejecución. Debe establecer explícitamente la propiedad [size](../../../ado/reference/ado-api/size-property-ado-parameter.md) para estos parámetros antes de llamar al método [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) para evitar errores.  
  
### <a name="fields"></a>Campos  
 El uso del método **Refresh** en la colección [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) no tiene ningún efecto visible. Para recuperar los cambios de la estructura de base de datos subyacente, debe utilizar el método [Requery](../../../ado/reference/ado-api/requery-method.md) o, si el objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) no admite marcadores, el método [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) .  
  
### <a name="properties"></a>Propiedades  
 El uso del método **Refresh** en una colección **Properties** de algunos objetos rellena la colección con las propiedades dinámicas que expone el proveedor. Estas propiedades proporcionan información sobre la funcionalidad específica del proveedor, más allá de las propiedades integradas que admite ADO.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Colección Axes](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)|[Colección de columnas](../../../ado/reference/adox-api/columns-collection-adox.md)|[Colección CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)|  
|[Colección de dimensiones](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)|[Colección de errores](../../../ado/reference/ado-api/errors-collection-ado.md)|[Colección Fields](../../../ado/reference/ado-api/fields-collection-ado.md)|  
|[Colección de grupos](../../../ado/reference/adox-api/groups-collection-adox.md)|[Colección Hierarchies](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)|[Colección de índices](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Colección de claves](../../../ado/reference/adox-api/keys-collection-adox.md)|[Colección de niveles](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)|[Colección de miembros](../../../ado/reference/ado-md-api/members-collection-ado-md.md)|  
|[Colección Parameters](../../../ado/reference/ado-api/parameters-collection-ado.md)|[Colección de posiciones](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)|[Colección de procedimientos](../../../ado/reference/adox-api/procedures-collection-adox.md)|  
|[Colección de propiedades](../../../ado/reference/ado-api/properties-collection-ado.md)|[Colección de tablas](../../../ado/reference/adox-api/tables-collection-adox.md)|[Recopilación de usuarios](../../../ado/reference/adox-api/users-collection-adox.md)|  
|[Colección de vistas](../../../ado/reference/adox-api/views-collection-adox.md)|||  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método Refresh (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Ejemplo del método Refresh (VC + +)](../../../ado/reference/ado-api/refresh-method-example-vc.md)   
 [Propiedad Count (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)
