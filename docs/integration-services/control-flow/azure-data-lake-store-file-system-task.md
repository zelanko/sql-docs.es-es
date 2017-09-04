---
title: "Tarea de sistema de archivos de almacén de Azure Data Lake | Documentos de Microsoft"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 303d3b74da3fe370d19b7602c0e11e67b63191e7
ms.openlocfilehash: ce2355de312faed9ab66991d6d0dd344ff315a55
ms.contentlocale: es-es
ms.lasthandoff: 08/29/2017

---
# <a name="azure-data-lake-store-file-system-task"></a>Tarea de sistema de archivos de almacén de Azure Data Lake

El **tarea de sistema de archivos de almacén de Azure datos Lake** permite a los usuarios realizar diversas operaciones del sistema de archivos en [Azure datos Lake almacén (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

El **tarea de sistema de archivos de almacén de Azure datos Lake** es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para agregar una tarea de sistema de archivos de almacén de Azure datos Lake a un paquete, arrástrelo desde el cuadro de herramientas de SSIS al lienzo del diseñador. A continuación, haga doble clic en la tarea, o haga clic en la tarea y seleccione **editar**para abrir el cuadro de diálogo del editor de tareas.

El **operación** propiedad especifica la operación del sistema de archivos para realizar. Se admiten las siguientes operaciones.

* **CopyToADLS:** cargar archivos a ADLS.
* **CopyFromADLS:** descargar archivos de ADLS.

Para cualquier operación, tendrá que especificar un administrador de conexiones de Azure Data Lake.

Estas son las descripciones de las propiedades específico a cada operación.

## <a name="copytoadls"></a>CopyToADLS
* **LocalDirectory:** especifica el directorio de origen que contiene archivos para cargar.
* **FileNamePattern:** especifica un filtro de nombre de archivo para archivos de código fuente. Sólo los archivos cuyo nombre coincida con el patrón especificado se cargará. Caracteres comodín `*` y `?` son compatibles.
* **SearchRecursively:** especifica si se debe buscar en el directorio de origen de archivos cargar de forma recursiva.
* **AzureDataLakeDirectory:** especifica el directorio de destino de ADLS para cargar archivos.
* **FileExpiry:** especifica una fecha de expiración y la hora para los archivos cargan en ADLS o deje en blanco para indicar que no expiren nunca los archivos de esta propiedad.

## <a name="copyfromadls"></a>CopyFromADLS
* **AzureDataLakeDirectory:** especifica el directorio de origen ADLS que contiene los archivos para descargar.
* **SearchRecursively:** especifica si se debe buscar en el directorio de origen de archivos descargar de forma recursiva.
* **LocalDirectory:** especifica el directorio de destino para almacenar los archivos descargados.
