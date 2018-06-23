---
title: Tarea Sistema de archivos de Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
caps.latest.revision: 3
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.openlocfilehash: 240780efd1b12596b0ebb6156ad98c508f0e8051
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103120"
---
# <a name="azure-data-lake-store-file-system-task"></a>Tarea Sistema de archivos de Azure Data Lake Store
El **tarea de sistema de archivos de almacén de Azure datos Lake** permite a los usuarios realizar diversas operaciones del sistema de archivos en [Azure datos Lake almacén (ADLS)](https://azure.microsoft.com/en-us/services/data-lake-store/).

Para agregar una tarea Sistema de archivos de Azure Data Lake Store a un paquete, arrástrela desde el cuadro de herramientas de SSIS al lienzo del diseñador. A continuación, haga doble clic en la tarea, o haga clic en la tarea y seleccione **editar**para abrir el cuadro de diálogo del editor de tareas.

La propiedad **Operación** especifica la operación del sistema de archivos que se va a realizar. Se admiten las siguientes operaciones.

* **CopyToADLS:** cargar archivos a ADLS.
* **CopyToADLS:** descargar archivos de ADLS.

Para cualquier operación, tendrá que especificar un administrador de conexiones de Azure Data Lake.

Estas son las descripciones de las propiedades específico a cada operación.

## <a name="copytoadls"></a>CopyToADLS
* **LocalDirectory:** especifica el directorio de origen que contiene archivos para cargar.
* **FileNamePattern:** especifica un filtro de nombre de archivo para los archivos de código fuente. Sólo los archivos cuyo nombre coincida con el patrón especificado se cargará. Se admite el uso de los caracteres comodín `*` y `?`.
* **SearchRecursively:** especifica si se deben buscar de forma recursiva en el directorio de origen los archivos para cargar.
* **AzureDataLakeDirectory:** especifica el directorio de destino de ADLS al que cargar archivos.
* **FileExpiry:** especifica una fecha de expiración y la hora para los archivos cargan en ADLS o deje en blanco para indicar que no expiren nunca los archivos de esta propiedad.

## <a name="copyfromadls"></a>CopyFromADLS
* **AzureDataLakeDirectory:** especifica el directorio de origen de ADLS que contiene los archivos que se descargarán.
* **SearchRecursively:** especifica si se deben buscar de forma recursiva en el directorio de origen archivos para descargar.
* **LocalDirectory:** especifica el directorio de destino para almacenar los archivos descargados.
