---
title: Método SubmitChanges (RDS) | Documentos de Microsoft
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
helpviewer_keywords:
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79b827d3288af7abcc59f063f80ff5e66e99d392
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="submitchanges-method-rds"></a>Método SubmitChanges (RDS)
Envía los cambios pendientes del localmente en caché y actualizables [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) al origen de datos especificado en el [conectar](../../../ado/reference/rds-api/connect-property-rds.md) propiedad o el [URL](../../../ado/reference/rds-api/url-property-rds.md) propiedad.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *Factory*  
 Una variable de objeto que representa un [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 *Conexión*  
 A **cadena** valor que representa la conexión creada con la **RDS. DataControl** del objeto [conectar](../../../ado/reference/rds-api/connect-property-rds.md) propiedad.  
  
 *Conjunto de registros*  
 Una variable de objeto que representa un **Recordset** objeto.  
  
## <a name="remarks"></a>Comentarios  
 El [conectar](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md), y [SQL](../../../ado/reference/rds-api/sql-property.md) propiedades deben establecerse antes de poder usar la **SubmitChanges** método con el  **RDS. DataControl** objeto.  
  
 Si se llama a la [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) método después de haber llamado **SubmitChanges** para el mismo **Recordset** objeto, el **CancelUpdate** se produce un error en la llamada porque ya se han confirmado los cambios.  
  
 Solo los registros modificados se envían para modificarlo y todos los cambios correctamente o con errores de todos los cambios entre sí.  
  
 Puede usar **SubmitChanges** sólo con el valor predeterminado **RDSServer.DataFactory** objeto. Objetos comerciales personalizados no pueden usar este método.  
  
 Si el **URL** se ha establecido la propiedad, **SubmitChanges** enviará los cambios en la ubicación especificada por la dirección URL.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método SubmitChanges (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [Botones de comando de libreta de direcciones](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)



