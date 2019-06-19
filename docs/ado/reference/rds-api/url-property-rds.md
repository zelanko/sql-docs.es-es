---
title: Propiedad de dirección URL (RDS) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: d5c1975e72a90defc15e4fcb41f0cfe44a714dc8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66697200"
---
# <a name="url-property-rds"></a>Propiedad de dirección URL (RDS)
Indica una cadena que contiene una dirección URL relativa o absoluta.  
  
 Puede establecer el **URL** propiedad en tiempo de diseño en el [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) del objeto de etiquetas, o en tiempo de ejecución de código de secuencias de comandos.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Design time: <PARAM NAME="URL" VALUE="Server">  
Run time: DataControl.URL="Server"  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Server*  
 Un **cadena** valor que contiene una dirección URL válida.  
  
 *DataControl*  
 Una variable de objeto que representa un **DataControl** objeto.  
  
## <a name="remarks"></a>Comentarios  
 Normalmente, la dirección URL identifica un archivo de páginas Active Server (.asp) que puede generar y devolver un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md). Por lo tanto, el usuario puede obtener un **Recordset** sin tener que invocar el lado servidor [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) ni programar un objeto de negocios personalizada.  
  
 Si el **URL** se ha establecido la propiedad, [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) enviará los cambios en la ubicación especificada por la dirección URL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de dirección URL (VBScript)](../../../ado/reference/rds-api/url-property-example-vbscript.md)


