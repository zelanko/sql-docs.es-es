---
title: Proveedores de datos utilizados para las conexiones de Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5ba97f90b877896d68cd62598f11d0845fb698e
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38057853"
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>Bibliotecas de cliente (proveedores de datos) para las conexiones de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services proporciona tres bibliotecas de cliente, también conocido como **proveedores de datos**, para el servidor y acceso a datos desde herramientas y aplicaciones de cliente. Herramientas como SSMS y SSDT y aplicaciones, tales como Power BI Desktop y Excel conectan a Analysis Services mediante el uso de estas bibliotecas. Dos de las bibliotecas de cliente, ADOMD.NET y Analysis Services Management Objects (AMO) son bibliotecas de cliente administradas. El proveedor OLE DB de Analysis Services (MSOLAP DLL) es una biblioteca de cliente nativo. Bibliotecas de cliente son los mismos para SQL Server Analysis Services y Azure Analysis Services.
  
##  <a name="bkmk_downloadsite"></a> Dónde obtener versiones más recientes  
 La versión instalada en un equipo cliente debe coincidir con la versión principal del servidor que proporciona los datos. Si la instalación del servidor es más reciente que los proveedores de datos instalados en las estaciones de trabajo de la red, quizás tenga que instalar bibliotecas más recientes.  

Bibliotecas de cliente incluidas en anteriores Feature Packs de SQL Server se corresponden con esa versión SQL; Sin embargo, puede no ser la versión más reciente. Conexión a Azure Analysis Services puede requerir que las versiones posteriores. Todas las versiones son compatibles con versiones anteriores.

Para obtener la versión más reciente, consulte [bibliotecas de cliente para conectarse a Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers). 
  
## <a name="see-also"></a>Vea también  
 [Conectar a Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
