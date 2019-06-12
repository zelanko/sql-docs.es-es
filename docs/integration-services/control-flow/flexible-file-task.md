---
title: Tarea de archivo flexible | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPEXTFILETASK.F1
- SQL14.DTS.DESIGNER.AFPEXTFILETASK.F1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2d01304a36f7676f53ffef3f6c6e3c600cb87cb6
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/30/2019
ms.locfileid: "66411102"
---
# <a name="flexible-file-task"></a>Tarea de archivo flexible

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

La tarea de archivo flexible permite a los usuarios realizar operaciones de archivo en varios servicios de almacenamiento compatibles.
Los servicios de almacenamiento admitidos actualmente son:

- Sistema de archivos local
- [Azure Blob Storage](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)

La tarea de archivo flexible es un componente del [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para agregar una tarea de archivo flexible a un paquete, arrástrela desde el cuadro de herramientas de SSIS al lienzo del diseñador. Después, haga doble clic en la tarea o haga clic con el botón derecho y seleccione **Editar**, para abrir el cuadro de diálogo **Flexible File Task Editor** (Editor de la tarea de archivo flexible).

La propiedad **Operación** especifica la operación de archivo que se va a realizar.
Actualmente solo se admite la operación de **copia**.

Para la operación de **copia**, están disponibles las propiedades siguientes.

- **SourceConnectionType:** especifica el tipo del administrador de conexiones de origen.
- **SourceConnection:** especifica el administrador de conexiones de origen.
- **SourceFolderPath:** especifica la ruta de acceso a la carpeta de origen.
- **SourceFileName:** especifica el nombre de archivo de origen. Si se deja en blanco, se copiará en la carpeta de origen.
- **SearchRecursively:** especifica si las subcarpetas se copian recursivamente.
- **DestinationConnectionType:** especifica el tipo del administrador de conexiones de destino.
- **DestinationConnection:** especifica el administrador de conexiones de destino.
- **DestinationFolderPath:** especifica la ruta de acceso a la carpeta de destino.
- **DestinationFileName:** especifica el nombre de archivo de destino.
