---
title: Propiedad URL (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- URL property [ADO]
ms.assetid: 8c56b233-1be8-442c-8d0e-a4c96465bc99
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c88b8029ee5d96986cf9b366bd8faee53ca1393b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67963223"
---
# <a name="url-property-rds"></a>Propiedad de dirección URL (RDS)
Indica una cadena que contiene una dirección URL relativa o absoluta.  
  
 Puede establecer la propiedad **URL** en tiempo de diseño en la etiqueta de objeto del objeto [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) , o en tiempo de ejecución en el código de scripting.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Server*  
 Valor de **cadena** que contiene una dirección URL válida.  
  
 *DataControl*  
 Variable de objeto que representa un objeto **DataControl** .  
  
## <a name="remarks"></a>Observaciones  
 Normalmente, la dirección URL identifica un archivo de página de Active Server (. asp) que puede generar y devolver un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md). Por lo tanto, el usuario puede obtener un **conjunto de registros** sin tener que invocar el objeto [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) del servidor o programar un objeto comercial personalizado.  
  
 Si se ha establecido la propiedad **URL** , [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) enviará los cambios a la ubicación especificada por la dirección URL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad de dirección URL (VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)


