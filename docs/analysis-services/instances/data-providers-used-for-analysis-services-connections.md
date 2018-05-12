---
title: Proveedores de datos utilizados para las conexiones de Analysis Services | Documentos de Microsoft
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
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>Bibliotecas de cliente (proveedores de datos) utilizadas para conexiones de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services proporciona tres bibliotecas de cliente, también conocido como **proveedores de datos**, para el acceso de datos de herramientas y aplicaciones de cliente y servidor. Herramientas como SSMS y SSDT y aplicaciones como Power BI Desktop y Excel se conectan a Analysis Services mediante el uso de estas bibliotecas. Dos de las bibliotecas de cliente, ADOMD.NET y Analysis Services Management Objects (AMO) son las bibliotecas de cliente administrado. El proveedor OLE DB de Analysis Services (MSOLAP DLL) es una biblioteca de cliente nativo. Bibliotecas de cliente son los mismos para SQL Server Analysis Services y Analysis Services de Azure.
  
##  <a name="bkmk_downloadsite"></a> Dónde obtener versiones más recientes  
 La versión instalada en un equipo cliente debe coincidir con la versión principal del servidor que proporciona los datos. Si la instalación del servidor es más reciente que los proveedores de datos instalados en las estaciones de trabajo de la red, quizás tenga que instalar bibliotecas más recientes.  

Bibliotecas de cliente incluidas en anteriores Feature Packs de SQL Server que se corresponden con esa versión SQL; Sin embargo, puede que no sean la versión más reciente. Conectarse a Analysis Services de Azure puede requerir que las versiones posteriores. Todas las versiones son compatibles con versiones anteriores.

Para obtener la versión más reciente, consulte [bibliotecas de cliente para conectarse a Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers). 
  
## <a name="see-also"></a>Vea también  
 [Conectar a Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
