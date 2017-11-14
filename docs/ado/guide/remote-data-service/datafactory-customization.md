---
title: "Personalización de DataFactory | Documentos de Microsoft"
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
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 044e738c69113740290843f14f0b2c14500307e1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="datafactory-customization"></a>Personalización de DataFactory
Servicio de datos remoto (RDS) proporciona una manera fácil tener acceso a datos en un sistema cliente/servidor de tres niveles. Un control de datos de cliente especifica los parámetros de cadena de conexión y comando para realizar una consulta en un origen de datos remoto o la cadena de conexión y [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) parámetros para realizar una actualización del objeto.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Los parámetros se pasan a un programa de servidor, que lleva a cabo la operación de acceso a datos en el origen de datos remoto. RDS proporciona un programa de servidor predeterminado denominado el [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto. El **RDSServer.DataFactory** object devuelve cualquier **Recordset** objeto generado por una consulta al cliente.  
  
 Sin embargo, el **RDSServer.DataFactory** se limita a realizar consultas y actualizaciones. No puede realizar validaciones ni procesamientos en las cadenas de conexión o un comando.  
  
 Con ADO, puede especificar que la **DataFactory** funcionan junto con otro tipo de programa de servidor denominado un *controlador*. Puede modificar el controlador de conexión de cliente y cadenas de comandos antes de que se usan para tener acceso al origen de datos. Además, el controlador puede exigir derechos de acceso, que rigen la capacidad del cliente para leer y escribir datos en el origen de datos.  
  
 Los parámetros que utiliza el controlador para modificar los parámetros de cliente y derechos de acceso se especifican en las secciones de un archivo de personalización.  
  
 Los temas siguientes proporcionan más información acerca de cómo personalizar la **DataFactory** objeto.  
  
-   [Descripción de los archivos de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [Sección Connect del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [Sección SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [Sección UserList del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [Opciones de cliente necesarias](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [Escribir su propio controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



