---
title: Origen de Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSSRC.F1
- SQL11.DTS.DESIGNER.AFPADLSSRC.F1
ms.assetid: 7d9e8457-62aa-4aea-98ee-7d1121dfae4f
caps.latest.revision: 6
author: yualan
ms.author: yual
manager: jhubbard
ms.openlocfilehash: e7bd327dc2657123daf94390785bda11a17e2040
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105182"
---
# <a name="azure-data-lake-store-source"></a>Origen de Azure Data Lake Store
  El componente **Origen de Azure Data Lake Store** permite que un paquete SSIS lea datos de un Azure Data Lake Store. Los formatos de archivo admitidos son: Text y Avro.
  
## <a name="configure-the-azure-data-lake-store-source"></a>Configurar Origen de Azure Data Lake Store 
  
1.  Para ver el editor del origen de Origen de Azure Data Lake Store, arrastre y coloque **Origen de Azure Data Lake Store** en el diseñador de flujos de datos y haga doble clic en él para abrir el editor.  
  
2.  En el campo **Administrador de conexiones de Azure Data Lake Store** , especifique un administrador de conexiones de Azure Data Lake Store o cree uno nuevo que haga referencia a un servicio de Azure Data Lake Store.  
  
    1.  Para el campo **Ruta de acceso del archivo** , especifique la ruta de acceso archivo de origen en Azure Data Lake Store.   
  
    2.  En el campo **Formato de archivo** , especifique el formato del archivo de origen.  
  
        Si el formato de archivo es Text, debe especificar el valor **Carácter de delimitador de columna** . Seleccione también **Nombres de columna de la primera fila de datos** si la primera fila del archivo contiene nombres de columna.  
  
3.  Después de especificar la información de conexión, cambie a la página **Columnas** para asignar columnas de origen a columnas de destino para el flujo de datos SSIS.  