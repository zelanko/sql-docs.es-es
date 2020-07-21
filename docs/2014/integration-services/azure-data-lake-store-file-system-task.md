---
title: Tarea Sistema de archivos de Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2d01c61521bf746076b359c65103e0ea46ec0f1b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439412"
---
# <a name="azure-data-lake-store-file-system-task"></a>Tarea Sistema de archivos de Azure Data Lake Store

La **tarea sistema de archivos Azure Data Lake Store** permite a los usuarios realizar varias operaciones del sistema de archivos en [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

Para agregar una tarea Sistema de archivos de Azure Data Lake Store a un paquete, arrástrela desde el cuadro de herramientas de SSIS al lienzo del diseñador. A continuación, haga doble clic en la tarea, o bien haga clic con el botón secundario en la tarea y seleccione **Editar**para abrir el cuadro de diálogo Editor de la tarea.

La propiedad **Operación** especifica la operación del sistema de archivos que se va a realizar. Es compatible con las siguientes operaciones.

* **CopyToADLS:** cargar archivos a ADLS.
* **CopyToADLS:** descargar archivos de ADLS.

Para cualquier operación, tendrá que especificar un administrador de conexiones de Azure Data Lake.

Estas son las descripciones de las propiedades específicas de cada operación.

## <a name="copytoadls"></a>CopyToADLS

* **LocalDirectory:** Especifica el directorio de origen que contiene los archivos que se van a cargar.
* **FileNamePattern:** especifica un filtro de nombre de archivo para los archivos de código fuente. Solo se cargarán los archivos cuyo nombre coincida con el patrón especificado. Se admite el uso de los caracteres comodín `*` y `?`.
* **SearchRecursively:** especifica si se deben buscar de forma recursiva en el directorio de origen los archivos para cargar.
* **AzureDataLakeDirectory:** especifica el directorio de destino de ADLS al que cargar archivos.
* **FileExpiry:** Especifica una fecha y hora de expiración para los archivos cargados en ADLS, o bien deje esta propiedad en blanco para indicar que los archivos nunca expiran.

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory:** especifica el directorio de origen de ADLS que contiene los archivos que se descargarán.
* **SearchRecursively:** especifica si se deben buscar de forma recursiva en el directorio de origen archivos para descargar.
* **LocalDirectory:** especifica el directorio de destino para almacenar los archivos descargados.
