---
title: Instalación de SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.reviewer: ''
ms.prod_service: database-engine
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cabd2d1ebbe726971e7837ff3e268ad3c2cee89f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72041261"
---
# <a name="installing-smo"></a>Instalar SMO

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

En esta página se proporciona información sobre cómo instalar SMO para que lo usen las aplicaciones de y los requisitos del sistema para usar SMO.

## <a name="smo-nuget-package"></a>Paquete NuGet de SMO

A partir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 2017 SMO se distribuye como el paquete de NuGet [Microsoft. SqlServer. SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) para permitir a los usuarios desarrollar aplicaciones con SMO.

Se trata de un reemplazo de SharedManagementObjects. msi, que se publicó previamente como parte de SQL Feature Pack para cada versión de SQL Server. Las aplicaciones que usan SMO deben actualizarse para usar el paquete NuGet en su lugar y serán responsables de asegurarse de que los archivos binarios se instalan con la aplicación que se está desarrollando.

>>[!Important]
>>Como se mencionó en la página [archivos y números de versión](files-and-version-numbers.md) , no debe instalar los ensamblados SMO en la GAC. Si lo hace, podrían producirse problemas con otras aplicaciones que también usan esas versiones de SMO [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (como Management Studio).

## <a name="installing-the-package"></a>Instalación del paquete

Consulte [Inicio rápido NuGet: usar un paquete](https://docs.microsoft.com/nuget/quickstart/use-a-package) para obtener instrucciones y ejemplos de instalación y uso de un paquete NuGet. 
  
## <a name="system-requirements"></a>Requisitos del sistema
  
 SMO requiere [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4,0 o .net Core 2,0 para ejecutarse, por lo que cualquier aplicación que lo use debe asegurarse de que los equipos cliente tengan instalada esa versión o superior. Algunos binarios nativos que se instalan con las bibliotecas SMO de NetFx también requieren la instalación del tiempo de ejecución de VC 2013. ese Runtime no se incluye en el paquete. Puede descargar el paquete redistribuible adecuado para su arquitectura de destino desdehttps://www.microsoft.com/download/details.aspx?id=40784
  
