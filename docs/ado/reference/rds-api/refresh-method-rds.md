---
title: Método Refresh (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9992b0f7e7281ec318f978ff487107fc832c961f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697524"
---
# <a name="refresh-method-rds"></a>Método Refresh (RDS)
Vuelve a consultar el origen de datos especificado en el [Connect](../../../ado/reference/rds-api/connect-property-rds.md) propiedad y las actualizaciones de los resultados de consulta.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
## <a name="remarks"></a>Comentarios  
 Debe establecer el [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md), y [SQL](../../../ado/reference/rds-api/sql-property.md) propiedades antes de usar el **actualizar** método. Todos los controles enlazados a datos en el formulario asociado con un **RDS. DataControl** objeto reflejará el nuevo conjunto de registros. Las preexistentes [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se libera el objeto y se descartan los cambios no guardados. El **actualizar** método convierte automáticamente el primer registro del registro actual.  
  
 Es una buena idea para llamar a la **actualizar** método periódicamente cuando se trabaja con datos. Si recuperar los datos y, a continuación, deje en un equipo cliente durante un tiempo, es probable que quede obsoleta. Es posible que los cambios que realice se producirá un error, porque otra persona podría haber cambiado el registro y enviado cambios.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Actualización de ejemplo del método (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Actualización de ejemplo del método (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [Botones de comando de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Actualizar (método) (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


