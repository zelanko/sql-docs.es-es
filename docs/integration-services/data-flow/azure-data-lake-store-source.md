---
title: Origen de Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSSRC.F1
- sql14.dts.designer.afpadlssrc.f1
ms.assetid: f9c3311f-7316-48d6-bf10-d810e70b4304
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 79cd70c9d36ab317ebf93f81203a0b1b9d77d008
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="azure-data-lake-store-source"></a>Origen de Azure Data Lake Store
  El componente **Origen de Azure Data Lake Store** permite que un paquete SSIS lea datos de un Azure Data Lake Store. Los formatos de archivo admitidos son: Text y Avro.
  
 El **Origen de Azure Data Lake Store** es un componente de [Feature Pack de SQL Server Integration Services (SSIS) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  
  
>   [!NOTE]
> Para garantizar que el Administrador de conexiones de Azure Data Lake Store y los componentes que lo utilizan (es decir, Origen de Data Lake Store y Destino de Azure Data Lake Store) se puedan conectar a los servicios, descargue la versión más reciente de Azure Feature Pack [aquí](https://www.microsoft.com/download/details.aspx?id=49492). 
  
## <a name="configure-the-azure-data-lake-store-source"></a>Configurar Origen de Azure Data Lake Store
 1. Para ver el editor del origen de Origen de Azure Data Lake Store, arrastre y coloque **Origen de Azure Data Lake Store** en el diseñador de flujos de datos y haga doble clic en él para abrir el editor.  
  
2.  En el campo **Administrador de conexiones de Azure Data Lake Store** , especifique un administrador de conexiones de Azure Data Lake Store o cree uno nuevo que haga referencia a un servicio de Azure Data Lake Store.  
  
    1.  Para el campo **Ruta de acceso del archivo** , especifique la ruta de acceso archivo de origen en Azure Data Lake Store.   
  
    2.  En el campo **Formato de archivo** , especifique el formato del archivo de origen.  
  
        Si el formato de archivo es Text, debe especificar el valor **Carácter de delimitador de columna** . Seleccione también **Nombres de columna de la primera fila de datos** si la primera fila del archivo contiene nombres de columna.  
  
3.  Después de especificar la información de conexión, cambie a la página **Columnas** para asignar columnas de origen a columnas de destino para el flujo de datos SSIS.   
