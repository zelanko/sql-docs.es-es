---
title: Tarea Sistema de archivos de Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aeabdcfa1fd36adf9bd4291623c56fbfecf0520e
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390253"
---
# <a name="azure-data-lake-store-file-system-task"></a>Tarea Sistema de archivos de Azure Data Lake Store

El **tarea sistema de archivos de Azure Data Lake Store** permite a los usuarios realizar diversas operaciones de sistema de archivos en [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

Para agregar una tarea Sistema de archivos de Azure Data Lake Store a un paquete, arrástrela desde el cuadro de herramientas de SSIS al lienzo del diseñador. A continuación, haga doble clic en la tarea, o haga clic en la tarea y seleccione **editar**para abrir el cuadro de diálogo del editor de tareas.

La propiedad **Operación** especifica la operación del sistema de archivos que se va a realizar. Se admiten las siguientes operaciones.

* **CopyToADLS:** Cargar archivos en ADLS.
* **CopyFromADLS:** Descargar archivos de ADLS.

Para cualquier operación, tendrá que especificar un administrador de conexiones de Azure Data Lake.

Estas son las descripciones de las propiedades específicas de cada operación.

## <a name="copytoadls"></a>CopyToADLS

* **LocalDirectory:** Especifica el directorio de origen que contiene archivos para cargar.
* **FileNamePattern:** Especifica un filtro de nombre de archivo para archivos de origen. Se cargará solo los archivos cuyo nombre coincide con el patrón especificado. Se admite el uso de los caracteres comodín `*` y `?`.
* **SearchRecursively:** Especifica si se debe buscar en el directorio de origen de archivos para cargar de forma recursiva.
* **AzureDataLakeDirectory:** Especifica el directorio de destino de ADLS para cargar archivos a.
* **FileExpiry:** Especifica una fecha de expiración y la hora de los archivos cargan en ADLS o dejar en blanco para indicar que no expiren nunca los archivos de esta propiedad.

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory:** Especifica el directorio de origen ADLS que contiene los archivos para descargar.
* **SearchRecursively:** Especifica si se debe buscar en el directorio de origen para descargar los archivos de forma recursiva.
* **LocalDirectory:** Especifica el directorio de destino para almacenar los archivos descargados.
