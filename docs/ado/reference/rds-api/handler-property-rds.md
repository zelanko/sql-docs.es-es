---
description: Propiedad de controlador (RDS)
title: Propiedad Handler (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
author: rothja
ms.author: jroth
ms.openlocfilehash: e80c140e5abab80e7c33199cb9401fe9d2774161
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438957"
---
# <a name="handler-property-rds"></a>Propiedad de controlador (RDS)
Indica el nombre de un programa de personalización de servidor (controlador) que extiende la funcionalidad de [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)y cualquier parámetro utilizado por el *controlador*.  
  
 **Se aplica a:** [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Variable de objeto que representa un objeto [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
 *String*  
 Valor de **cadena** que contiene el nombre del controlador y cualquier parámetro, separados por comas (por ejemplo, `"handlerName,parm1,parm2,...,parm` *N* `"` ).  
  
## <a name="remarks"></a>Observaciones  
 Esta propiedad admite la [Personalización](../../../ado/guide/remote-data-service/datafactory-customization.md), una funcionalidad que requiere el establecimiento de la propiedad [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) en **adUseClient**.  
  
 El nombre del controlador y sus parámetros, si los hay, se separan mediante comas (","). Se producirá un comportamiento imprevisible si un punto y coma (";") aparece en cualquier parte de la *cadena*. Puede escribir su propio controlador, siempre que admita la interfaz **IDataFactoryHandler** .  
  
 El nombre del controlador predeterminado es **MSDFMAP. **Y su parámetro predeterminado es un archivo de personalización denominado **MSDFMAP.INI**. Utilice esta propiedad para invocar los archivos de personalización alternativos creados por el administrador del servidor.  
  
 La alternativa a establecer la propiedad del **controlador** es especificar un controlador y parámetros en la propiedad [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) ; es decir, "**handler =**_handlerName, parámetro1, parámetro2,...;_".  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad de controlador (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


