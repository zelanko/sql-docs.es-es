---
title: Propiedad de controlador (RDS) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5cba5a709933f89cb7bb19666140053cd6cfc94
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="handler-property-rds"></a>Propiedad de controlador (RDS)
Indica el nombre de un programa de personalización de servidor (controlador) que amplía la funcionalidad de la [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)y todos los parámetros utilizados por la *controlador*.  
  
 **Se aplica a:** [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *String*  
 A **cadena** valor que contiene el nombre del controlador y los parámetros, todas separadas por comas (por ejemplo, `"handlerName,parm1,parm2,...,parm` *N*`"`).  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad es compatible con [personalización](../../../ado/guide/remote-data-service/datafactory-customization.md), una funcionalidad que requiera una configuración de la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient**.  
  
 El nombre del controlador y sus parámetros, si los hay, están separados por comas (","). Se producirá un comportamiento imprevisible si un punto y coma (";") aparece en cualquier lugar dentro de *cadena*. Puede escribir su propio controlador siempre que admita la **IDataFactoryHandler** interfaz.  
  
 El nombre del controlador predeterminado es **MSDFMAP. Controlador**, y su parámetro predeterminado es un archivo de personalización denominado **MSDFMAP. INI**. Utilice esta propiedad para invocar los archivos de personalización alternativos creados por el administrador del servidor.  
  
 La alternativa a la configuración de la **controlador** propiedad consiste en especificar un controlador y parámetros en el [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad; es decir, "**controlador = *** handlerName, parámetro1, parámetro2,...;* ".  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de controlador (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [Personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


