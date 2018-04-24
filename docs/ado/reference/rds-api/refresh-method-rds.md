---
title: Método Refresh (RDS) | Documentos de Microsoft
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 89e9088aeec78213f7da9a79ba78255de4b94b97
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="refresh-method-rds"></a>Método Refresh (RDS)
Vuelve a consultar el origen de datos especificado en el [conectar](../../../ado/reference/rds-api/connect-property-rds.md) propiedad y las actualizaciones de los resultados de la consulta.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
## <a name="remarks"></a>Comentarios  
 Debe establecer el [conectar](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md), y [SQL](../../../ado/reference/rds-api/sql-property.md) propiedades antes de usar el **actualizar** método. Todos los controles enlazados a datos en el formulario asociado con un **RDS. DataControl** objeto reflejará el nuevo conjunto de registros. Las preexistentes [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se libera el objeto y se descartan los cambios no guardados. El **actualizar** método convierte automáticamente el primer registro el registro actual.  
  
 Es una buena idea para llamar a la **actualizar** método periódicamente cuando se trabaja con datos. Si recuperar datos y, a continuación, lo deja en un equipo cliente durante un tiempo, es probable que quede obsoleta. Es posible que los cambios que realice se producirá un error, ya que otra persona podría haber cambiado el registro y enviado cambios antes de.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Actualización de ejemplo del método (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Actualización de ejemplo del método (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [Botones de comando de libreta de direcciones](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Actualizar (método, ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


