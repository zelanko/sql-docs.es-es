---
title: Destino de DataReader | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.datareaderdest.f1
helpviewer_keywords:
- DataReader destination
- destinations [Integration Services], DataReader
ms.assetid: 56fcc4bf-c901-42c3-a71d-110039293431
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 694e85a56686379d089f3c2fc11721e4dd6f8642
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62827549"
---
# <a name="datareader-destination"></a>DataReader, destino
  El destino de DataReader expone los datos en un flujo de datos mediante la interfaz ADO.NET `DataReader`. En ese momento los datos pueden ser usados por otras aplicaciones. Por ejemplo, puede configurar el origen de datos de un informe de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para usar el resultado de la ejecución de un paquete de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para ello, se crea un flujo de datos que implementa el destino de DataReader.  
  
 Para obtener información sobre cómo acceder a valores y leerlos en el destino de DataReader mediante programación, vea [Cargar la salida de un paquete local](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md).  
  
## <a name="configuration-of-the-datareader-destination"></a>Configuración del destino de DataReader  
 Puede especificar un valor de tiempo de espera para el destino de DataReader e indicar si se produce un error en el destino al agotarse el tiempo de espera. El tiempo de espera se agota si la aplicación no pide datos dentro del tiempo especificado.  
  
 El destino de DataReader tiene una entrada. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](../common-properties.md)  
  
-   [Propiedades personalizadas del destino DataReader](datareader-destination-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md).  
  
  
