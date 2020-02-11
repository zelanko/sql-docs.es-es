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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67963288"
---
# <a name="submitchanges-method-rds"></a>Método SubmitChanges (RDS)
Envía los cambios pendientes del [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) actualizado en caché local al origen de datos especificado en la propiedad [Connect](../../../ado/reference/rds-api/connect-property-rds.md) o la propiedad [URL](../../../ado/reference/rds-api/url-property-rds.md) .  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.SubmitChanges DataFactory.SubmitChanges Connection, Recordset  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Variable de objeto que representa un objeto [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
 *DataFactory*  
 Variable de objeto que representa un objeto [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) .  
  
 *Connection*  
 Valor de **cadena** que representa la conexión creada con el **objeto RDS. **Propiedad [Connect](../../../ado/reference/rds-api/connect-property-rds.md) del objeto DataControl.  
  
 *DataRecordsets*  
 Variable de objeto que representa un objeto de **conjunto de registros** .  
  
## <a name="remarks"></a>Observaciones  
 Se deben establecer las propiedades [Connect](../../../ado/reference/rds-api/connect-property-rds.md), [Server](../../../ado/reference/rds-api/server-property-rds.md)y [SQL](../../../ado/reference/rds-api/sql-property.md) antes de poder utilizar el método **SubmitChanges** con **RDS. Objeto DataControl** .  
  
 Si llama al método [CancelUpdate](../../../ado/reference/rds-api/cancelupdate-method-rds.md) después de haber llamado a **SubmitChanges** para el mismo objeto de **conjunto de registros** , se produce un error en la llamada a **CancelUpdate** porque los cambios ya se han confirmado.  
  
 Solo se envían los registros modificados para su modificación, y todos los cambios se realizan correctamente, o bien todos los cambios tienen errores juntos.  
  
 Solo puede utilizar **SubmitChanges** con el objeto **RDSServer. DataFactory** predeterminado. Los objetos comerciales personalizados no pueden utilizar este método.  
  
 Si se ha establecido la propiedad **URL** , **SubmitChanges** enviará los cambios a la ubicación especificada por la dirección URL.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo del método SubmitChanges (VBScript)](../../../ado/reference/rds-api/submitchanges-method-example-vbscript.md)   
 [Botones de comando de la libreta de direcciones](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [Método CancelUpdate (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)



