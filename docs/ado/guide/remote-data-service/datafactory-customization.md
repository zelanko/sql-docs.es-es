---
title: Personalización de DataFactory | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory customization in RDS [ADO]
ms.assetid: 86d77985-a0d0-405a-8587-c85a20540a0e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 52cb60fc8d0c214bbc3d827617cf088a89b2aa83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704295"
---
# <a name="datafactory-customization"></a>Personalización de DataFactory
Servicio de datos remoto (RDS) proporciona una manera de realizar fácilmente el acceso a datos en un sistema cliente/servidor de tres niveles. Un control de datos de cliente especifica los parámetros de cadena de conexión y comando para realizar una consulta en un origen de datos remoto o la cadena de conexión y [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) parámetros para realizar una actualización de objeto.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Los parámetros se pasan a un programa de servidor, que realiza la operación de acceso a datos en el origen de datos remoto. RDS proporciona un programa de servidor predeterminado denominado el [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto. El **RDSServer.DataFactory** objeto devuelve un valor cualquiera **Recordset** objeto producido por una consulta al cliente.  
  
 Sin embargo, el **RDSServer.DataFactory** se limita a realizar consultas y actualizaciones. No puede realizar ninguna validación o el procesamiento de las cadenas de conexión o un comando.  
  
 Con ADO, puede especificar que el **DataFactory** profesional junto con otro tipo de programa de servidor denominado un *controlador*. El controlador puede modificar cadenas de comandos y de conexión de cliente antes de que se usan para tener acceso al origen de datos. Además, el controlador puede exigir derechos de acceso que rigen la capacidad del cliente para leer y escribir datos en el origen de datos.  
  
 Los parámetros que utiliza el controlador para modificar los parámetros de cliente y los derechos de acceso se especifican en las secciones de un archivo de personalización.  
  
 Los temas siguientes proporcionan más información sobre cómo personalizar el **DataFactory** objeto.  
  
-   [Descripción del archivo de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [Sección de conexión del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [Sección de SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [Sección UserList del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [Configuración de cliente requerida](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


