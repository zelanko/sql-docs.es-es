---
title: Conectarse a Azure Blob Storage (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7287d5d1342da6c2a43e7013eae60247cf4aabaf
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>Conectarse a Azure Blob Storage (Asistente para importación y exportación de SQL Server)
En este tema se muestra cómo conectarse a un origen de datos de **Azure Blob Storage** desde la página **Elegir un origen de datos** o **Elegir un destino** del Asistente para importación y exportación de SQL Server.

>   [!NOTE]
> Para usar el origen o el destino del blob de Azure, tiene que instalar Azure Feature Pack para SQL Server Integration Services.
> - Para descargar el Feature Pack, consulte [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=49492) (Azure Feature Pack para Microsoft SQL Server 2016 Integration Services).
>
> - Para obtener más información, vea [Azure Feature Pack para Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

En la captura de pantalla siguiente se muestran las opciones para configurar una conexión a Azure Blob Storage.

![conexión de Almacenamiento de blobs de Azure](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>Opciones que hay que especificar

> [!NOTE]
> Las opciones de conexión de este proveedor de datos son las mismas independientemente de si Azure Blob Storage es el origen o el destino. Es decir, las opciones que ve son las mismas en las páginas **Elegir un origen de datos** y **Elegir un destino** del asistente.

 **Usar una cuenta de Azure**  
 Especifique si usa una cuenta en línea.
  
 **Nombre de la cuenta de almacenamiento**  
 Escriba el nombre de la cuenta de almacenamiento de Azure.  
  
**Clave de cuenta**  
Escriba la clave de la cuenta de almacenamiento de Azure.  
  
 **Usar HTTPS**  
 Especifique si desea utilizar HTTP o HTTPS para conectarse a la cuenta de almacenamiento.  
  
 **Usar cuenta de desarrollador local**  
 Especifique si desea utilizar el emulador de almacenamiento en el equipo local.  
  
 **Nombre del contenedor de blob**  
 Seleccione uno en la lista de contenedores de almacenamiento disponibles en la cuenta de almacenamiento especificada.  
  
 **Formato de archivo de blob**  
 Seleccione el formato de archivo de texto o Avro.  
  
 **Carácter delimitador de columna**  
 Si selecciona el formato de texto, escriba el carácter delimitador de columna.  
  
 **Usar la primera fila como nombres de columna**  
 Especifique si la primera fila de datos contiene nombres de columna.  

## <a name="see-also"></a>Vea también
[Choose a Data Source](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md) (Selección de un origen de datos)  
[Choose a Destination](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md) (Selección de un destino)

