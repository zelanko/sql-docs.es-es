---
title: Objeto DataSpace (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 078799f90a0241dc29f30693adce95ea2e795ff8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654273"
---
# <a name="dataspace-object-rds"></a>Objeto DataSpace (RDS)
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Crea objetos proxy de cliente a objetos de negocios personalizados que se encuentra en el nivel intermedio.  
  
 Servicio de datos remotos necesita a servidores proxy de objetos de negocio para que los componentes del lado cliente puedan comunicarse con objetos de negocios que se encuentra en el nivel intermedio. Servidores proxy facilitan el empaquetado, desempaquetado y del transporte (serialización) de la aplicación [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) datos a través de límites de proceso o del equipos.  
  
 Servicio de datos remoto usa el **RDS. DataSpace** del objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método para crear servidores proxy de objetos de negocios. El proxy del objeto de negocios se crea dinámicamente cada vez que se crea una instancia de su equivalente de objetos empresariales de nivel medio. Servicio de datos remoto admite los siguientes protocolos: HTTP, HTTPS (HTTP Secure Sockets), DCOM y en proceso (los componentes de cliente y el objeto de negocios que residen en el mismo equipo).  
  
> [!NOTE]
>  RDS se comporta de forma "independiente" cuando el **RDS. DataSpace** objeto utiliza los protocolos HTTP o HTTPS. Es decir, se descarta cualquier información interna sobre una solicitud de cliente después de que el servidor devuelve una respuesta.  
  
> [!NOTE]
>  Aunque parezca que el objeto de negocios existe durante la vigencia del proxy del objeto de negocio, el objeto de negocios realmente existe sólo hasta que se envía una respuesta a una solicitud. Cuando se emite una solicitud (es decir, se invoca un método en el objeto de negocios), el proxy abre una nueva conexión con el servidor y el servidor crea una nueva instancia del objeto comercial. Después de que el objeto de negocios responde a la solicitud, el servidor destruye el objeto de negocios y cierra la conexión.  
  
> [!NOTE]
>  Este comportamiento significa que no se puede pasar datos de una solicitud a otra mediante una propiedad de objeto de negocios o una variable. Debe emplear algún otro mecanismo, como un archivo o un argumento de método, para conservar los datos de estado.  
  
 El identificador de clase para el **RDS. DataSpace** objeto es BD96C556-65A3 - 11 D 0-983A-00C04FC29E36.  
  
 El **DataSpace** objeto es seguro para scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades del objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [DataSpace y el ejemplo del método CreateObject (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


