---
title: "Tarea de sistema de archivos de almacén de Azure Data Lake | Documentos de Microsoft"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: douglasl
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
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 4cb0585acf73e734662847401c60686b54ae6410
ms.contentlocale: es-es
ms.lasthandoff: 10/10/2017

---
# <a name="azure-data-lake-store-file-system-task"></a>Tarea de sistema de archivos de almacén de Azure Data Lake

La tarea de sistema de archivos de almacén de Azure datos Lake permite a los usuarios realizar diversas operaciones del sistema de archivos en [Azure datos Lake almacén (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

La tarea de sistema de archivos de almacén de Azure datos Lake es un componente de la [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

## <a name="configure-the-azure-data-lake-store-file-system-task"></a>Configurar la tarea sistema de archivos de almacén de Azure Data Lake

Para agregar una tarea de sistema de archivos de almacén de Azure datos Lake a un paquete, arrástrelo desde el cuadro de herramientas de SSIS al lienzo del diseñador. A continuación, haga doble clic en la tarea, o haga clic en la tarea y seleccione **editar**para abrir el **Editor de tareas del sistema de archivos de almacén de Azure datos Lake** cuadro de diálogo.

El **operación** propiedad especifica la operación del sistema de archivos para realizar. Seleccione una de las siguientes operaciones:

- **CopyToADLS:** cargar archivos a ADLS.
- **CopyFromADLS:** descargar archivos de ADLS.

Para cualquier operación, tendrá que especificar un administrador de conexiones de Azure Data Lake.

Estas son las propiedades específicas de cada operación:

### <a name="copytoadls"></a>CopyToADLS
- **LocalDirectory:** especifica el directorio de origen local que contiene los archivos para cargar.
- **FileNamePattern:** especifica un filtro de nombre de archivo para archivos de código fuente. Se cargan sólo los archivos cuyo nombre coincida con el patrón especificado. Caracteres comodín `*` y `?` son compatibles.
- **SearchRecursively:** especifica si se debe buscar en el directorio de origen de archivos cargar de forma recursiva.
- **AzureDataLakeDirectory:** especifica el directorio de destino de ADLS para cargar archivos.
- **FileExpiry:** especifica una fecha de expiración y la hora de los archivos se cargan en ADLS. Deje esta propiedad en blanco para indicar que los archivos nunca expiran.

### <a name="copyfromadls"></a>CopyFromADLS
- **AzureDataLakeDirectory:** especifica el directorio de origen ADLS que contiene los archivos para descargar.
- **SearchRecursively:** especifica si se debe buscar en el directorio de origen de archivos descargar de forma recursiva.
- **LocalDirectory:** especifica el directorio de destino para almacenar los archivos descargados.
