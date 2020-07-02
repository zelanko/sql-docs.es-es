---
title: Componentes
description: Obtenga información sobre los componentes de la SQL Server Native Client como sqlncli11.dll, sqlnclir11. RLL, SQLNCLI. h y sqlncli11. lib.
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
ms.openlocfilehash: a221c926a0af32af050f01ef17f87d329486e61e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85657749"
---
# <a name="components-of-sql-server-native-client"></a>Componentes de SQL Server Native Client
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client contiene los componentes siguientes:  
  
|Componente|Descripción|  
|---------------|-----------------|  
|sqlncli11.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene toda la funcionalidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Esto incluye el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlnclir11.rll|El archivo de recursos adjunto para la biblioteca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|   
|sqlncli.h|El archivo de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que contiene todas las definiciones nuevas necesarias para utilizar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Este archivo de encabezado reemplaza a los archivos de encabezado odbcss.h y sqloledb.h.<br /><br /> Nota: no puede hacer referencia a SQLNCLI. h y odbcss. h en el mismo programa, pero puede hacer referencia a SQLNCLI. h y SQLOLEDB. h en el mismo programa, siempre que se defina primero SQLOLEDB. h.|  
|sqlncli11.lib|El archivo de biblioteca necesario para llamar directamente a las funciones de la utilidad **BCP** que forman parte del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client.<br /><br /> Nota: Si hace referencia al archivo sqlncli11. lib en el código de programación, debe asegurarse de que el archivo de sqlncli11.dll está en la ruta de acceso del sistema y en la ruta de acceso del sistema de los usuarios que usan la aplicación.|  
  
## <a name="see-also"></a>Consulte también  
 [Generar aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
