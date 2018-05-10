---
title: Destino de DataReader | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
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
- sql13.dts.designer.datareaderdest.f1
helpviewer_keywords:
- DataReader destination
- destinations [Integration Services], DataReader
ms.assetid: 56fcc4bf-c901-42c3-a71d-110039293431
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d31006d561e50bfd765108a685fef826b97a2bf2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="datareader-destination"></a>DataReader, destino
  El destino de DataReader expone los datos en un flujo de datos mediante la interfaz ADO.NET **DataReader** . En ese momento los datos pueden ser usados por otras aplicaciones. Por ejemplo, puede configurar el origen de datos de un informe de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para usar el resultado de la ejecución de un paquete de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para ello, se crea un flujo de datos que implementa el destino de DataReader.  
  
 Para obtener información sobre cómo acceder a valores y leerlos en el destino de DataReader mediante programación, vea [Cargar la salida de un paquete local](../../integration-services/run-manage-packages-programmatically/loading-the-output-of-a-local-package.md).  
  
## <a name="configuration-of-the-datareader-destination"></a>Configuración del destino de DataReader  
 Puede especificar un valor de tiempo de espera para el destino de DataReader e indicar si se produce un error en el destino al agotarse el tiempo de espera. El tiempo de espera se agota si la aplicación no pide datos dentro del tiempo especificado.  
  
 El destino de DataReader tiene una entrada. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas del destino DataReader](../../integration-services/data-flow/datareader-destination-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  
