---
title: "Conectarse al almacenamiento de blobs de Azure (importación de SQL Server y Asistente para exportación) | Documentos de Microsoft"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 36b992b5141799d4e168b2e990643e6a515a8d69
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>Conectarse al almacenamiento de blobs de Azure (importación de SQL Server y Asistente para exportación)
Este tema muestra cómo conectarse a un **almacenamiento de blobs de Azure** del origen de datos de la **elegir un origen de datos** o **elegir un destino** página de la importación de SQL Server y el Asistente para exportación.

>   [!NOTE]
> Para utilizar el origen de blobs de Azure o el destino, tendrá que instalar el Feature Pack de Azure para SQL Server Integration Services.
> - Para descargar el Feature Pack, consulte [Microsoft SQL Server 2016 Integration Services Feature Pack para Azure](https://www.microsoft.com/download/details.aspx?id=49492).
>
> - Para obtener más información, vea [Azure Feature Pack para Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

La captura de pantalla siguiente muestra las opciones de configuración para una conexión al almacenamiento de blobs de Azure.

![conexión de Almacenamiento de blobs de Azure](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>Opciones para especificar

> [!NOTE]
> Las opciones de conexión para este proveedor de datos son los mismos si el almacenamiento de blobs de Azure es el origen o el destino. Es decir, las opciones que ve son los mismos en ambos el **elegir un origen de datos** y **elegir un destino** páginas del asistente.

 **Usar una cuenta de Azure**  
 Especifique si usa una cuenta en línea.
  
 **Nombre de la cuenta de almacenamiento**  
 Escriba el nombre de la cuenta de almacenamiento de Azure.  
  
**Clave de cuenta**  
Escriba la clave para la cuenta de almacenamiento de Azure.  
  
 **Usar HTTPS**  
 Especifique si desea utilizar HTTP o HTTPS para conectarse a la cuenta de almacenamiento.  
  
 **Usar cuenta de desarrollador local**  
 Especifique si desea utilizar el emulador de almacenamiento en el equipo local.  
  
 **Nombre del contenedor de blob**  
 Seleccione uno en la lista de contenedores de almacenamiento disponibles en la cuenta de almacenamiento especificada.  
  
 **Formato de archivo de blob**  
 Seleccione el formato de archivo de texto o Avro.  
  
 **Carácter delimitador de columna**  
 Si selecciona el formato de texto, escriba el carácter de delimitador de columna.  
  
 **Usar la primera fila como nombres de columna**  
 Especifique si la primera fila de datos contiene nombres de columna.  

## <a name="see-also"></a>Vea también
[Elija un origen de datos](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Elegir un destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


