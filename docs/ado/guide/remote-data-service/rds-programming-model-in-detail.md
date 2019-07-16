---
title: Modelo de programación de RDS en detalle | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO], details
ms.assetid: 3e57af8d-519b-4467-a0bd-af468534cefd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d7251e3a403168e8383e636a8e6b5f712b9f7bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922524"
---
# <a name="rds-programming-model-in-detail"></a>Modelo detallado de programación de RDS
Estos son los elementos clave del modelo de programación de RDS:  
  
-   RDS. Espacio de datos  
  
-   RDSServer.DataFactory  
  
-   RDS. Control de datos  
  
-   Evento  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="rdsdataspace"></a>RDS. Espacio de datos  
 La aplicación cliente debe especificar el servidor y el programa de servidor para invocar. En cambio, la aplicación recibe una referencia al programa de servidor y puede tratar la referencia como si fuera el propio programa de servidor.  
  
 El modelo de objetos RDS incluye esta funcionalidad con el [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto.  
  
 El programa de servidor se especifica con un identificador de programa, o *ProgID*. El servidor usa el *ProgID* y del registro del equipo servidor para buscar información sobre el programa real para iniciar.  
  
 RDS hace una distinción interna dependiendo de si el programa de servidor está en un servidor remoto a través de Internet o una intranet; un servidor en una red de área local; o no en un servidor en absoluto, sino en una biblioteca de vínculos dinámicos (DLL) local. Esta distinción determina cómo se intercambia entre el cliente y el servidor de información y marca una diferencia tangible en el tipo de referencia que se devuelven a la aplicación cliente. Sin embargo, desde el punto de vista, esta distinción tiene ningún significado especial. Lo único que importa es que reciba una referencia de programa utilizable.  
  
## <a name="rdsserverdatafactory"></a>RDSServer.DataFactory  
 RDS proporciona un programa de servidor predeterminado que puede realizar una consulta SQL en el origen de datos y volver una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) de objeto o tomar una **Recordset** objeto y actualizar el origen de datos.  
  
 El modelo de objetos RDS incluye esta funcionalidad con el [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 Además, este objeto tiene un método para crear un valor vacío **Recordset** objeto que se puede rellenar mediante programación ([CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md)) y otro método para convertir un **conjunto de registros**  objeto en una cadena de texto para crear una página Web ([ConvertToString](../../../ado/reference/rds-api/converttostring-method-rds.md)).  
  
 Con ADO, puede reemplazar algunas de las conexiones estándar y el comportamiento de comando de la **RDSServer.DataFactory** con un **DataFactory** controlador y un archivo de personalización que contiene la conexión, comando y los parámetros de seguridad.  
  
 El programa de servidor se denomina a veces un *objeto comercial*. Puede escribir su propio objeto de negocios personalizada que puede realizar el acceso a datos complicadas, comprobaciones de validez y así sucesivamente. Incluso al escribir un objeto comercial personalizado, puede crear una instancia de un **RDSServer.DataFactory** de objetos y usar algunas de sus métodos para realizar sus propias tareas.  
  
## <a name="rdsdatacontrol"></a>RDS. Control de datos  
 RDS proporciona un medio para combinar la funcionalidad de la **RDS. DataSpace** y **RDSServer.DataFactory**y también permiten controles visuales utilizar fácilmente la **Recordset** objeto devuelto por una consulta desde un origen de datos. Intentos de RDS, para que el caso más común para realizar tanto como sea posible para obtener acceso a información en un servidor y mostrarlos en un control visual automáticamente.  
  
 El modelo de objetos RDS incluye esta funcionalidad con el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 El **RDS. DataControl** tiene dos aspectos. Un aspecto pertenece al origen de datos. Si establece el comando y la información de conexión con el **Connect** y **SQL** propiedades de la **RDS. DataControl**, usarán automáticamente la **RDS. DataSpace** para crear una referencia al valor predeterminado **RDSServer.DataFactory** objeto. El **RDSServer.DataFactory** usará el **Connect** valor de propiedad para conectarse al origen de datos, use el **SQL** valor de propiedad para obtener un  **Conjunto de registros** desde el origen de datos y devolver el **Recordset** de objeto para el **RDS. DataControl**.  
  
 El segundo aspecto pertenece a la presentación de devuelto **Recordset** información en un control visual. Puede asociar un control visual con el **RDS. DataControl** (en un proceso llamado enlace) y obtener acceso a la información de asociado **Recordset** objeto, mostrar los resultados de consulta en una página Web de Microsoft® Internet Explorer. Cada **RDS. DataControl** objeto enlaza una **Recordset** objeto que representa los resultados de una sola consulta, a uno o varios controles visuales (por ejemplo, un cuadro de texto, cuadro combinado, control de cuadrícula y así sucesivamente). Puede haber más de uno **RDS. DataControl** objeto en cada página. Cada **RDS. DataControl** objeto se puede conectar a un origen de datos diferentes y contener los resultados de una consulta independiente.  
  
 El **RDS. DataControl** objeto también tiene sus propios métodos para explorar, ordenar y filtrar las filas del asociado **Recordset** objeto. Estos métodos son similares, pero no igual que con los métodos de ADO **Recordset** objeto.  
  
## <a name="events"></a>Events  
 RDS admite dos de sus propios eventos, que son independientes del modelo de eventos de ADO. El [onReadyStateChange](../../../ado/reference/rds-api/onreadystatechange-event-rds.md) se llama al evento cada vez que el **RDS. DataControl** [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) los cambios de propiedad, lo que le avise cuando se haya completado correctamente una operación asincrónica, finalizado o ha experimentado un error. El [onError](../../../ado/reference/rds-api/onerror-event-rds.md) se llama al evento cada vez que se produce un error, incluso si el error se produce durante una operación asincrónica.  
  
> [!NOTE]
>  Microsoft Internet Explorer proporciona dos eventos adicionales a RDS: **onDataSetChanged**, lo que indica que el **Recordset** es funcional pero sigue recuperando filas, y  **onDataSetComplete**, lo que indica que el **Recordset** ha terminado de recuperar filas.  
  
## <a name="see-also"></a>Vea también  
 [Modelo de programación de RDS con objetos](../../../ado/guide/remote-data-service/rds-programming-model-with-objects.md)   
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [Escenario RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial de RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Seguridad y uso de RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



