---
title: Método SubmitChanges (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SubmitChanges method [ADO]
ms.assetid: 250062a4-13c4-4bed-807d-8b9ad81536d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 783ad55a2355759f7625d536272f5243cd1c61c4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963288"
---
# <a name="submitchanges-method-rds"></a>Método SubmitChanges (RDS)
Envía los cambios pendientes del localmente en caché y actualizable [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) al origen de datos especificado en el [Connect](../../../ado/reference/rds-api/connect-property-rds.md) propiedad o el [URL](../../../ado/reference/rds-api/url-property-rds.md) propiedad.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *DataFactory*  
 Una variable de objeto que representa un [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 *Conexión*  
 Un **cadena** valor que representa la conexión creada con el **RDS. DataControl** del objeto [Connect](../../../ado/reference/rds-api/connect-property-rds.md) propiedad.  
  
 *Recordset*  
 Una variable de objeto que representa un **Recordset** objeto.  
  
## <a name="remarks"></a>Comentarios  
 El [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md), y [SQL](../../../ado/reference/rds-api/sql-property.md) propiedades deben establecerse antes de poder usar el **SubmitChanges** método con el  **RDS. DataControl** objeto.  
  
 Si se llama a la [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) método después de haber llamado **SubmitChanges** para el mismo **Recordset** objeto, el **CancelUpdate** se produce un error en la llamada porque ya se han confirmado los cambios.  
  
 Solo los registros modificados se envían para la modificación y todos los cambios se realizan correctamente o todos los cambios dan error juntas.  
  
 Puede usar **SubmitChanges** sólo con el valor predeterminado **RDSServer.DataFactory** objeto. Objetos de negocios personalizados no pueden usar este método.  
  
 Si el **URL** se ha establecido la propiedad, **SubmitChanges** enviará los cambios en la ubicación especificada por la dirección URL.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método SubmitChanges (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [Botones de comando de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)



