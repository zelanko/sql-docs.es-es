---
title: Propiedad del servidor (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: add581048739a6ba12dc046d2f9362816b661687
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680629"
---
# <a name="server-property-rds"></a>Propiedad del servidor (RDS)
Indica el protocolo de nombre y la comunicación de Internet Information Services (IIS).  
  
 Puede establecer el **Server** propiedad en tiempo de diseño en las etiquetas de objeto de la[RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) de objeto o en tiempo de ejecución de código de secuencias de comandos.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
 **HTTP**  
  
 Sintaxis de tiempo de diseño  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 Sintaxis de tiempo de ejecución  
  
```  
  
DataControl  
.Server="http://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 Sintaxis de tiempo de diseño  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 Sintaxis de tiempo de ejecución  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 Sintaxis de tiempo de diseño  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 Sintaxis de tiempo de ejecución  
  
```  
  
DataControl.Server="computername"  
```  
  
 **En curso**  
  
 Sintaxis de tiempo de diseño  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 Sintaxis de tiempo de ejecución  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>Parámetros  
 *awebsrvr*o *computername*  
 Un **cadena** valor que contiene una Internet o la ruta de acceso de intranet o el nombre del equipo, si el servidor está en un equipo remoto; o bien, una cadena vacía si el servidor está en el equipo local.  
  
 *port*  
 Opcional. Un puerto que se usa para conectarse a un servidor que ejecuta IIS. El número de puerto se establece en el Explorador de Internet (en el **vista** menú, haga clic en **opciones**y, a continuación, seleccione el **conexión** pestaña) o en IIS.  
  
 *DataControl*  
 Una variable de objeto que representa un **RDS. DataControl** objeto.  
  
## <a name="remarks"></a>Comentarios  
 El servidor es la ubicación donde el **RDS. DataControl** se procesa la solicitud (es decir, una consulta o actualización). De forma predeterminada, todas las solicitudes se procesan mediante el [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto, [MSDFMAP. Controlador](../../../ado/guide/remote-data-service/datafactory-customization.md) componente, y [MSDFMAP. INI](../../../ado/guide/remote-data-service/understanding-the-customization-file.md) archivo en el servidor especificado. Recuerde que al cambiar de servidores para reconciliar la configuración de los antiguos y nuevos **MSDFMAP. INI** archivos. Las incompatibilidades pueden hacer solicitudes que se realice correctamente en un servidor a un error en otro. Si se establece la propiedad del servidor en la cadena vacía "", estos objetos se usará en el equipo local.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de servidor (VBScript)](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [Propiedad Connect (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Propiedad SQL](../../../ado/reference/rds-api/sql-property.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


