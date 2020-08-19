---
description: Personalización de DataFactory
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b7ec3707df187e09de92fa42d7ed2b1c1b8e1130
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452227"
---
# <a name="datafactory-customization"></a>Personalización de DataFactory
El servicio de datos remotos (RDS) proporciona una manera sencilla de realizar el acceso a los datos en un sistema cliente/servidor de tres niveles. Un control de datos de cliente especifica los parámetros de cadena de conexión y de comando para realizar una consulta en un origen de datos remoto, o parámetros de objeto de [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) y de cadena de conexión para realizar una actualización.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Los parámetros se pasan a un programa de servidor, que realiza la operación de acceso a datos en el origen de datos remoto. RDS proporciona un programa de servidor predeterminado denominado objeto [RDSServer. DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) . El objeto **RDSServer. DataFactory** devuelve cualquier objeto de **conjunto de registros** generado por una consulta al cliente.  
  
 Sin embargo, el **RDSServer. DataFactory** se limita a realizar consultas y actualizaciones. No puede realizar ninguna validación o procesamiento en las cadenas de conexión o comando.  
  
 Con ADO, puede especificar que el **DataFactory** funcione junto con otro tipo de programa de servidor denominado *controlador*. El controlador puede modificar las cadenas de conexión de cliente y de comando antes de que se usen para obtener acceso al origen de datos. Además, el controlador puede aplicar derechos de acceso, que rigen la capacidad del cliente para leer y escribir datos en el origen de datos.  
  
 Los parámetros que utiliza el controlador para modificar los parámetros de cliente y los derechos de acceso se especifican en secciones de un archivo de personalización.  
  
 En los temas siguientes se proporciona más información sobre cómo personalizar el objeto **DataFactory** .  
  
-   [Descripción del archivo de personalización](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)  
  
-   [Sección de conexión del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-connect-section.md)  
  
-   [Sección de SQL del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-sql-section.md)  
  
-   [Sección UserList del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)  
  
-   [Sección de registros del archivo de personalización](../../../ado/guide/remote-data-service/customization-file-logs-section.md)  
  
-   [Configuración de cliente requerida](../../../ado/guide/remote-data-service/required-client-settings.md)  
  
-   [Escritura de un controlador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


