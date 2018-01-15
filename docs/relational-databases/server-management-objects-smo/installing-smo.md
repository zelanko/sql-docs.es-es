---
title: Instalar SMO | Documentos de Microsoft
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: sql
ms.prod_service: database-engine
ms.component: smo
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
caps.latest.revision: "46"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 26438c3a9baea978aace0fc1383349f813e6c0d0
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2018
---
#<a name="installing-smo"></a>Instalar SMO

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

Esta página proporciona información sobre cómo instalar SMO para su uso por las aplicaciones y los requisitos del sistema para usar SMO.

## <a name="smo-nuget-package"></a>Paquete de NuGet SMO

A partir de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 SMO se distribuye como el [Microsoft.SqlServer.SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) paquete NuGet para permitir a los usuarios a desarrollar aplicaciones con SMO.

Se trata de un reemplazo para SharedManagementObjects.msi, que se publicaron anteriormente como parte del Feature Pack de SQL para cada versión de SQL Server. Las aplicaciones que usan SMO deben actualizarse para utilizar el paquete de NuGet en su lugar y serán responsables de garantizar que los archivos binarios se instalan con la aplicación que se está desarrollada.

>>[!Important]
>>Como se mencionó en la [archivos y números de versión](files-and-version-numbers.md) página, no debe instalar los ensamblados SMO en la GAC. Si lo hace, podría causar problemas con otras aplicaciones que también usan esas versiones de SMO (como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio).

##<a name="installing-the-package"></a>Instalar el paquete

Vea [inicio rápido de NuGet - Use un paquete](https://docs.microsoft.com/en-us/nuget/quickstart/use-a-package) para obtener instrucciones y ejemplos de instalación y uso de un paquete de NuGet. 
  
## <a name="system-requirements"></a>Requisitos del sistema
  
 SMO requiere [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.0 se ejecutan, por lo que las aplicaciones que usen deben asegurarse de que los equipos cliente tienen esa versión o superior instalado.
  
