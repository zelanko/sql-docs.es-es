---
title: Destino de Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 06/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSDEST.F1
- SQL11.DTS.DESIGNER.AFPADLSDEST.F1
ms.assetid: d0e86032-2a6b-48b2-898f-e94328474fde
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: ebf686807169bb850e5a3ae8fac8cfb0b8ca7791
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061458"
---
# <a name="azure-data-lake-store-destination"></a>Destino de Azure Data Lake Store
  El componente **Destino de Azure Data Lake Store** permite que un paquete SSIS escriba datos en un Azure Data Lake Store. Los formatos de archivo admitidos son: Text, Avro y ORC. 
  
## <a name="configure-the-azure-data-lake-store-destination"></a>Configurar Destino de Azure Data Lake Store 

1. Arrastre y coloque **Destino de Azure Data Lake Store** en el diseñador de flujos de datos y haga doble clic en él para ver el editor.  

2.  En el campo **Administrador de conexiones de Azure Data Lake Store** , especifique un administrador de conexiones de Azure Data Lake Store o cree uno nuevo que haga referencia a un servicio de Azure Data Lake Store.  
  
    1.  En el campo **Ruta de acceso del archivo** , especifique el nombre de archivo en el que quiere escribir datos. Si el archivo ya existe, se sobrescribirá su contenido.  
  
    2.  En el campo **Formato de archivo** , especifique el formato que quiere utilizar.  
  
        Si el formato de archivo es texto, debe especificar el valor del **carácter delimitador de columna** . Seleccione también **nombres de columna en la primera fila de datos** si la primera fila del archivo contiene nombres de columna.  

        Si el formato de archivo es ORC, debe instalar JRE de la plataforma correspondiente. 
  
3.  Después de especificar la información de conexión, cambie a la página **Columnas** para asignar columnas de origen a columnas de destino para el flujo de datos SSIS.  
