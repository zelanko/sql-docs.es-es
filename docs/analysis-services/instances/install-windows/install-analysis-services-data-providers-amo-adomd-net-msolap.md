---
title: Instalar proveedores de datos de Analysis Services (AMO, ADOMD.NET, MSOLAP) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a7aedabc-6af9-4698-a7a4-98f894001476
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd6aa812228cce132b4180a8537ba853f3ea92a2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="install-analysis-services-data-providers-amo-adomdnet-msolap"></a>Instalar proveedores de datos de Analysis Services (AMO, ADOMD.NET, MSOLAP)
  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] es una actualización de versión de los proveedores de datos de Analysis Services, que consta de ADOMD.Net, AMO y MSOLAP.  
  
 Para la mayoría de escenarios de acceso a datos basados en consultas, puede usar las versiones anteriores existentes de los proveedores de datos que ya están instaladas en los sistemas cliente para obtener acceso a los modelos tabulares y multidimensionales en una instancia de Analysis Services de SQL Server 2016, incluidos los modelos tabulares que usen características exclusivas de SQL Server 2016. Como norma general, las aplicaciones cliente que generan consultas, como Excel, Reporting Services o Tableau, no requieren los proveedores de datos más recientes al obtener acceso a un modelo de Analysis Services.  
  
 Las herramientas de modelado y administración son una excepción a la regla, al menos en cuanto a requisitos de versión para proveedores de datos. Estas herramientas deben tener los proveedores de datos que se han diseñado específicamente para el servidor de destino con el fin de manipular objetos en ese servidor. Afortunadamente, las herramientas que se suministran con [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] incluyen de forma automática proveedores de datos que se ajustan a la versión actual del servidor.  El programa de instalación de SQL Server Data Tools para Visual Studio 2015 instala proveedores de datos de SQL Server 2016 Analysis Services. De forma similar, SQL Server 2016 Management Studio, que usa tanto AMO como ADOMD.Net, instala ambos proveedores de datos con destino [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 Un escenario que requiere una instalación manual de un proveedor de datos es el de aplicaciones personalizadas o scripts que usan objetos de administración de Analysis Services (AMO). Esta versión introduce un espacio de nombres refactorizado que mueve los objetos principales, como Server y Database, a un nuevo espacio de nombres (Microsoft.AnalysisServices.Core) que forma parte del ensamblado Microsoft.AnalysisServices.dll. Si tiene código o scripts personalizados que usan AMO, debe volver a compilar el código y actualizar manualmente los AMO en cada servidor y estación de trabajo cliente que realiza una conexión directa a través de AMO a una instancia de SQL Server 2016 de Analysis Services.  
  
## <a name="provider-list"></a>Lista de proveedores  
 Estos proveedores se describen en la tabla siguiente.  
  
||||  
|-|-|-|  
|Proveedor|Nombre de archivo|Versión|  
|Objetos de administración de Analysis Services (AMO)|Microsoft.AnalysisServices.dll|13.0.0.0|  
|Analysis Services Core|Microsoft.AnalysisServices.Core.dll|13.0.0.0|  
|Analysis Services (ADOMD.NET)|Microsoft.AnalysisServices.AdomdClient.dll|13.0.0.0|  
|Proveedor OLE DB para Analysis Services (MSOLAP)|MSOLAP130.dll|13.0.0.0|  
  
## <a name="download-and-install-data-provider"></a>Descargar e instalar el proveedor de datos  
  
1.  Vaya a la [página de descarga de Feature Pack de SQL Server 2016](http://go.microsoft.com/fwlink/?LinkID=398150).  
  
2.  Haga clic en **Descargar** para habilitar la instalación de los componentes individuales.  
  
3.  Para equipos de 64 bits, seleccione todos o algunos de los siguientes (de lo contrario, elija el equivalente de x86):  
  
    -   ENU\x64\SQL_AS_ADOMD.msi  
  
    -   ENU\x64\SQL_AS_AMO.msi  
  
    -   ENU\x64\SQL_AS_OLEDB.msi  
  
4.  Haga clic en **Siguiente** para descargar los archivos.  
  
5.  Ejecute cada programa para instalar el proveedor. Los ensamblados ADO.MD y AMO se instalan en C:\Windows\assembly\GAC_MSIL. El proveedor OLE DB de Analysis Services se instala en C:\Archivos de programa\Microsoft Analysis Services\AS OLEDB\130.  
  
## <a name="verify-installation"></a>Comprobar la instalación  
  
1.  En el explorador de archivos, vaya a C:\Windows\Assembly.  
  
2.  Haga clic con el botón derecho en Microsoft.AnalysisServices y seleccione **Propiedades**.  
  
3.  Haga clic en **Versión** para confirmar que tiene la compilación más reciente.  
  
  

