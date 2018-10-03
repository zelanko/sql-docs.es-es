---
title: Tarea Sistema de archivos de Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0c6b4c27b0edde310ba3252dd67bf8f51f40f0e5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48136565"
---
# <a name="azure-data-lake-store-file-system-task"></a>Tarea Sistema de archivos de Azure Data Lake Store
El **tarea sistema de archivos de Azure Data Lake Store** permite a los usuarios realizar diversas operaciones de sistema de archivos en [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/en-us/services/data-lake-store/).

Para agregar una tarea Sistema de archivos de Azure Data Lake Store a un paquete, arrástrela desde el cuadro de herramientas de SSIS al lienzo del diseñador. A continuación, haga doble clic en la tarea, o haga clic en la tarea y seleccione **editar**para abrir el cuadro de diálogo del editor de tareas.

La propiedad **Operación** especifica la operación del sistema de archivos que se va a realizar. Se admiten las siguientes operaciones.

* **CopyToADLS:** cargar archivos a ADLS.
* **CopyToADLS:** descargar archivos de ADLS.

Para cualquier operación, tendrá que especificar un administrador de conexiones de Azure Data Lake.

Estas son las descripciones de las propiedades específicas de cada operación.

## <a name="copytoadls"></a>CopyToADLS
* **LocalDirectory:** especifica el directorio de origen que contiene archivos para cargar.
* **FileNamePattern:** especifica un filtro de nombre de archivo para los archivos de código fuente. Se cargará solo los archivos cuyo nombre coincide con el patrón especificado. Se admite el uso de los caracteres comodín `*` y `?`.
* **SearchRecursively:** especifica si se deben buscar de forma recursiva en el directorio de origen los archivos para cargar.
* **AzureDataLakeDirectory:** especifica el directorio de destino de ADLS al que cargar archivos.
* **FileExpiry:** especifica una fecha de expiración y una hora para los archivos cargan en ADLS o dejar en blanco para indicar que no expiren nunca los archivos de esta propiedad.

## <a name="copyfromadls"></a>CopyFromADLS
* **AzureDataLakeDirectory:** especifica el directorio de origen de ADLS que contiene los archivos que se descargarán.
* **SearchRecursively:** especifica si se deben buscar de forma recursiva en el directorio de origen archivos para descargar.
* **LocalDirectory:** especifica el directorio de destino para almacenar los archivos descargados.
