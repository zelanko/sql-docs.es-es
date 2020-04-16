---
title: Componentes
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0c824d145b6353f96a3756f28b7446799b303889
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388214"
---
# <a name="components-of-sql-server-native-client"></a>Componentes de SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client contiene los componentes siguientes:  
  
|Componente|Descripción|  
|---------------|-----------------|  
|sqlncli11.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene toda la funcionalidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Esto incluye el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlnclir11.rll|El archivo de recursos adjunto para la biblioteca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|   
|sqlncli.h|El archivo de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que contiene todas las definiciones nuevas necesarias para utilizar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Este archivo de encabezado reemplaza a los archivos de encabezado odbcss.h y sqloledb.h.<br /><br /> Nota: No puede hacer referencia a sqlncli.h y odbcss.h en el mismo programa, pero puede hacer referencia a sqlncli.h y sqloledb.h en el mismo programa siempre que sqloledb.h se defina primero.|  
|sqlncli11.lib|El archivo de biblioteca **bcp** necesario para llamar directamente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a las funciones de utilidad bcp que forman parte del controlador ODBC de Native Client.<br /><br /> Nota: Si hace referencia al archivo sqlncli11.lib en el código de programación, debe asegurarse de que el archivo sqlncli11.dll está en la ruta de acceso del sistema y en la ruta de acceso del sistema de los usuarios que hacen uso de la aplicación.|  
  
## <a name="see-also"></a>Consulte también  
 [Generar aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
