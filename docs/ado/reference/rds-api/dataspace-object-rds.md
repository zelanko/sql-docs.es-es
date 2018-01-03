---
title: Objeto DataSpace (RDS) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 05dde8ebc5f0f9ab859ed5ada8ff366af8ce5302
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="dataspace-object-rds"></a>Objeto DataSpace (RDS)
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Crea servidores proxy de cliente a objetos comerciales personalizados ubicados en el nivel intermedio.  
  
 El servicio de datos remotos necesita a servidores proxy de objetos de negocio para que los componentes del lado cliente pueden comunicarse con objetos de negocio ubicados en el nivel intermedio. Servidores proxy facilitan el empaquetado, desempaquetado y del transporte (serialización) de la aplicación [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) datos a través de límites de procesos o equipos.  
  
 Servicio de datos remoto usa el **RDS. DataSpace** del objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método para crear servidores proxy de objetos de negocios. El proxy del objeto de negocio se crea dinámicamente cada vez que se crea una instancia de su homólogo del objeto comercial de nivel medio. Servicio de datos remoto admite los protocolos siguientes: HTTP, HTTPS (HTTP Secure Sockets), DCOM y en proceso (los componentes de cliente y el objeto de negocio que residen en el mismo equipo).  
  
> [!NOTE]
>  RDS se comporta de forma "independiente" cuando el **RDS. DataSpace** objeto usa los protocolos HTTP o HTTPS. Es decir, se descarta toda la información interna sobre una solicitud de cliente después de que el servidor devuelve una respuesta.  
  
> [!NOTE]
>  Aunque parezca que el objeto de negocio existe durante la vigencia del proxy del objeto de negocios, el objeto comercial existe realmente solo hasta que se envía una respuesta a una solicitud. Cuando se emite una solicitud (es decir, se invoca un método en el objeto de negocio), el proxy abre una nueva conexión al servidor y el servidor crea una nueva instancia del objeto comercial. Después de que el objeto de negocio responde a la solicitud, el servidor destruye el objeto de negocios y cierra la conexión.  
  
> [!NOTE]
>  Este comportamiento significa que no se puede pasar datos de una solicitud a otra mediante una propiedad de objeto de negocios o variable. Debe emplear algún otro mecanismo, como un archivo o un argumento de método, para conservar los datos de estado.  
  
 El identificador de clase para el **RDS. DataSpace** objeto es BD96C556-65A3 - 11 D 0-983A-00C04FC29E36.  
  
 El **DataSpace** objeto es seguro para scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades del objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [DataSpace y el ejemplo del método CreateObject (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


