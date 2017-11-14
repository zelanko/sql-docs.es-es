---
title: "Modelo de programación de RDS detalladamente | Documentos de Microsoft"
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
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db8a1222c560b54629baa34da595e0f5c49835b0
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="rds-programming-model-in-detail"></a>Modelo de programación de RDS en detalle
Éstos son los elementos clave del modelo de programación de RDS:  
  
-   RDS. Espacio de datos  
  
-   RDSServer.DataFactory  
  
-   RDS. DataControl  
  
-   Evento  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="rdsdataspace"></a>RDS. Espacio de datos  
 La aplicación cliente debe especificar el servidor y el programa de servidor para invocar. En cambio, la aplicación recibe una referencia al programa de servidor y puede tratar la referencia como si fuera el propio programa de servidor.  
  
 El modelo de objetos RDS incluye esta funcionalidad con el [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto.  
  
 El programa de servidor se especifica con un identificador de programa, o *ProgID*. El servidor usa el *ProgID* y el registro del equipo servidor para buscar información acerca del programa real para iniciar.  
  
 RDS hace una distinción interna dependiendo de si el programa de servidor está en un servidor remoto a través de Internet o en una intranet; un servidor en una red de área local; en un servidor, pero en su lugar en una biblioteca de vínculos dinámicos (DLL) local. Esta distinción determina cómo se intercambia entre el cliente y el servidor de información y afecta de manera tangible en el tipo de referencia que se devuelven a la aplicación cliente. Sin embargo, desde el punto de vista, esta distinción no tiene ningún significado especial. Todo lo que es importante es que reciba una referencia de programa utilizable.  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 RDS proporciona un programa de servidor predeterminado que puede realizar una consulta SQL en el origen de datos y se devuelve un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) de un objeto o tomar una **Recordset** objeto y actualizar el origen de datos.  
  
 El modelo de objetos RDS incluye esta funcionalidad con el [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 Además, este objeto tiene un método para crear vacío **Recordset** objeto que se puede rellenar mediante programación ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)) y otro método para convertir un **conjunto de registros**  objeto en una cadena de texto para crear una página Web ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md)).  
  
 Con ADO, puede invalidar algunas de las conexiones estándar y el comportamiento de comando de la **RDSServer.DataFactory** con un **DataFactory** controlador y un archivo de personalización que contiene la conexión, comando y los parámetros de seguridad.  
  
 El programa de servidor se denomina a veces un *objeto comercial*. Puede escribir su propio objeto comercial personalizado que puede realizar el acceso a datos complicado, comprobaciones de validez y así sucesivamente. Incluso cuando se escribe un objeto comercial personalizado, puede crear una instancia de un **RDSServer.DataFactory** objeto y usar algunos de sus métodos para realizar sus propias tareas.  
  
## <a name="rdsdatacontrol"></a>RDS. DataControl  
 RDS proporciona un medio para combinar la funcionalidad de la **RDS. DataSpace** y **RDSServer.DataFactory**y también permiten que los controles visuales utilizar fácilmente la **Recordset** objeto devuelto por una consulta desde un origen de datos. Intentos de RDS, en el caso más común, hacer tanto como sea posible para obtener acceso a información de un servidor y mostrarlos en un control visual automáticamente.  
  
 El modelo de objetos RDS incluye esta funcionalidad con el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 El **RDS. DataControl** tiene dos aspectos. Un aspecto pertenece al origen de datos. Si establece el comando y la información de conexión mediante el **conectar** y **SQL** propiedades de la **RDS. DataControl**, utilizará automáticamente el **RDS. DataSpace** para crear una referencia en el valor predeterminado **RDSServer.DataFactory** objeto. La **RDSServer.DataFactory** usará la **conectar** valor de propiedad para conectarse al origen de datos, use la **SQL** valor de propiedad para obtener un  **Conjunto de registros** desde el origen de datos y se devuelve el **Recordset** el objeto a la **RDS. DataControl**.  
  
 El segundo aspecto pertenece a la presentación de devuelto **Recordset** información en un control visual. Puede asociar un control visual con el **RDS. DataControl** (en un proceso llamado enlace) y obtener acceso a la información en el asociado **Recordset** objeto, mostrar los resultados de la consulta en una página Web en Microsoft® Internet Explorer. Cada **RDS. DataControl** objeto enlaza una **Recordset** objeto, que representa los resultados de una sola consulta, en uno o más controles visuales (por ejemplo, un cuadro de texto, un cuadro combinado, un control de cuadrícula etc.). Puede haber más de un **RDS. DataControl** objeto en cada página. Cada **RDS. DataControl** objeto puede estar conectado a un origen de datos diferente y contiene los resultados de una consulta independiente.  
  
 El **RDS. DataControl** objeto también tiene sus propios métodos para explorar, ordenar y filtrar las filas del asociado **Recordset** objeto. Estos métodos son similares, pero no es igual que los métodos de la propiedad ADO **Recordset** objeto.  
  
## <a name="events"></a>Eventos  
 RDS admite dos de sus propios eventos, que son independientes del modelo de eventos de ADO. El [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) eventos se llama cada vez que la **RDS. DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) cambios de propiedad, lo que le avise cuando se haya completado correctamente una operación asincrónica, finaliza o se ha producido un error. El [onError](../../../ado/reference/rds-api/onerror-event-rds.md) eventos se llaman cada vez que se produce un error, incluso si el error se produce durante una operación asincrónica.  
  
> [!NOTE]
>  Microsoft Internet Explorer proporciona dos eventos adicionales a RDS: **onDataSetChanged**, lo que indica que la **Recordset** es funcional pero sigue recuperando filas, y  **onDataSetComplete**, lo que indica que la **Recordset** ha terminado de recuperar filas.  
  
## <a name="see-also"></a>Vea también  
 [Modelo de programación de RDS con objetos](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Escenario RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Seguridad y el uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)




