---
title: "Modelo de programación básico de RDS | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS programming model [ADO]
ms.assetid: 0bdd236b-edff-4aac-94c3-93e1465ca6c5
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d99d092b91ed150a3ad9163f2c4f7e513554e9f4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="basic-rds-programming-model"></a>Modelo de programación de RDS básica
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS orienta a las aplicaciones que existen en el siguiente entorno: una aplicación cliente especifica un programa que se ejecutará en un servidor y los parámetros necesarios para devolver la información deseada. El programa que se invoca en el servidor obtiene acceso al origen de datos especificado, recupera la información, procesa opcionalmente los datos y, a continuación, devuelve la información resultante a la aplicación de cliente en un formulario que puede utilizar fácilmente. RDS proporciona los medios para realizar la siguiente secuencia de acciones:  
  
-   Especifique el programa que se invocará en el servidor y obtenga un medio para hacer referencia a él desde el cliente. (Esta referencia se denomina a veces un *proxy*. Representa el programa de servidor remoto. La aplicación de cliente "llamará" el proxy como si fuese un programa local, pero invoca en realidad el programa de servidor remoto.)  
  
-   Invocar el programa de servidor. Pasar parámetros al programa de servidor que identifican el origen de datos y el comando para emitir. (El programa de servidor realmente utiliza ADO para tener acceso al origen de datos. ADO establece una conexión con uno de los parámetros especificados y, a continuación, emite el comando especificado en el otro parámetro.)  
  
-   El programa de servidor obtiene un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto desde el origen de datos. Si lo desea, el **Recordset** objeto se procesa en el servidor.  
  
-   El programa de servidor devuelve el estado final **Recordset** objeto a la aplicación cliente.  
  
-   En el cliente, el **Recordset** objeto se coloca en un formulario que se puede utilizar fácilmente mediante controles visuales.  
  
-   Las modificaciones a la **Recordset** objeto se envían hacia el programa de servidor, que se usa para actualizar el origen de datos.  
  
 Este modelo de programación contiene algunas características prácticas. Si no es necesario un programa de servidor complejo para tener acceso al origen de datos y si proporciona los parámetros de comando y conexión necesaria, RDS configurará automáticamente y recuperar los datos especificados con un programa del servidor simple, de forma predeterminada.  
  
 Si necesita un procesamiento más complejo, puede especificar su propio programa de servidor personalizado. Por ejemplo, dado que un programa de servidor personalizado tiene toda la funcionalidad de ADO a su disposición, podría conectarse a varios orígenes de datos, combinar sus datos de alguna manera compleja y, a continuación, devolver un resultado simple, que se procesa a la aplicación cliente.  
  
 Por último, si sus necesidades son intermedias, ADO admite ahora la personalización del comportamiento del programa de servidor predeterminado.  
  
## <a name="see-also"></a>Vea también  
 [Modelo de programación de RDS en detalle](../../../ado/guide/remote-data-service/rds-programming-model-in-detail.md)   
 [Escenario RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Seguridad y uso de RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



