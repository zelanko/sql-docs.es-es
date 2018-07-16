---
title: Destino de Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSDEST.F1
- SQL11.DTS.DESIGNER.AFPADLSDEST.F1
ms.assetid: d0e86032-2a6b-48b2-898f-e94328474fde
caps.latest.revision: 5
author: yualan
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7ca00d765a0279a70f0758a917ce51343e7be362
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37272211"
---
# <a name="azure-data-lake-store-destination"></a>Destino de Azure Data Lake Store
  El componente **Destino de Azure Data Lake Store** permite que un paquete SSIS escriba datos en un Azure Data Lake Store. Los formatos de archivo admitidos son: Text, Avro y ORC. 
  
## <a name="configure-the-azure-data-lake-store-destination"></a>Configurar Destino de Azure Data Lake Store 

1. Arrastre y coloque **Destino de Azure Data Lake Store** en el diseñador de flujos de datos y haga doble clic en él para ver el editor.  

2.  En el campo **Administrador de conexiones de Azure Data Lake Store** , especifique un administrador de conexiones de Azure Data Lake Store o cree uno nuevo que haga referencia a un servicio de Azure Data Lake Store.  
  
    1.  En el campo **Ruta de acceso del archivo** , especifique el nombre de archivo en el que quiere escribir datos. Si el archivo ya existe, se sobrescribirá su contenido.  
  
    2.  En el campo **Formato de archivo** , especifique el formato que quiere utilizar.  
  
        Si el formato de archivo es Text, debe especificar el valor **Carácter de delimitador de columna** . Seleccione también **Nombres de columna de la primera fila de datos** si la primera fila del archivo contiene nombres de columna.  

        Si el formato de archivo es ORC, debe instalar JRE de la plataforma correspondiente. 
  
3.  Después de especificar la información de conexión, cambie a la página **Columnas** para asignar columnas de origen a columnas de destino para el flujo de datos SSIS.  
