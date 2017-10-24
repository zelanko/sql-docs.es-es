---
title: Propiedad del servidor (RDS) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 05ff98ce99d444a9b5dfc1aac035920a29482d7c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="server-property-rds"></a>Propiedad del servidor (RDS)
Indica el protocolo de nombre y la comunicación de Internet Information Services (IIS).  
  
 Puede establecer la **Server** propiedad en tiempo de diseño en las etiquetas de objeto de la[RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) de objeto o en tiempo de ejecución en código de scripting.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
 **HTTP**  
  
 Sintaxis en tiempo de diseño  
  
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
  
 Sintaxis en tiempo de diseño  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 Sintaxis de tiempo de ejecución  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 Sintaxis en tiempo de diseño  
  
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
  
 Sintaxis en tiempo de diseño  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 Sintaxis de tiempo de ejecución  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>Parámetros  
 *awebsrvr*o *NombreDeEquipo*  
 A **cadena** valor que contiene un Internet o la ruta de acceso de intranet o el nombre del equipo, si el servidor está en un equipo remoto; o bien, una cadena vacía si el servidor está en el equipo local.  
  
 *port*  
 Opcional. Un puerto que se utiliza para conectarse a un servidor que ejecuta IIS. El número de puerto se establece en Internet Explorer (en el **vista** menú, haga clic en **opciones**y, a continuación, seleccione la **conexión** ficha) o en IIS.  
  
 *DataControl*  
 Una variable de objeto que representa un **RDS. DataControl** objeto.  
  
## <a name="remarks"></a>Comentarios  
 El servidor es la ubicación donde el **RDS. DataControl** se procesa la solicitud (es decir, una consulta o actualización). De forma predeterminada, todas las solicitudes se procesan por el [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto, [MSDFMAP. Controlador](../../../ado/guide/remote-data-service/datafactory-customization.md) componente, y [MSDFMAP. INI](../../../ado/guide/remote-data-service/understanding-the-customization-file.md) archivo en el servidor especificado. Recuerde que al cambiar de servidores para reconciliar la configuración de los antiguos y nuevos **MSDFMAP. INI** archivos. Las incompatibilidades pueden hacer solicitudes que se realizan correctamente en un servidor genere un error en otro. Si se establece la propiedad del servidor en la cadena vacía "", estos objetos se usará en el equipo local.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad de servidor (VBScript)](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [Propiedad Connect (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Propiedad SQL](../../../ado/reference/rds-api/sql-property.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)



