---
title: Componentes de SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- data access [SQL Server Native Client], components
- components [SQL Server Native Client]
- SQLNCLI, about SQL Server Native Client
ms.assetid: 65f932d5-daa1-4eff-b6df-ee633fcf2a7c
author: rothja
ms.author: jroth
ms.openlocfilehash: 32438b9fb5473d9251acd0aceddb46db373f3548
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85017649"
---
# <a name="components-of-sql-server-native-client"></a>Componentes de SQL Server Native Client
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client contiene los componentes siguientes:  
  
|Componente|Descripción|  
|---------------|-----------------|  
|sqlncli11.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene toda la funcionalidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Esto incluye el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlnclir11.rll|El archivo de recursos adjunto para la biblioteca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|s10ch_sqlncli.chm|El archivo de ayuda del Asistente para orígenes de datos que documenta cómo crear un origen de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client o el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|sqlncli.h|El archivo de encabezado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que contiene todas las definiciones nuevas necesarias para utilizar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Este archivo de encabezado reemplaza a los archivos de encabezado odbcss.h y sqloledb.h. **Nota:**  No se puede hacer referencia a SQLNCLI. h y odbcss. h en el mismo programa, pero se puede hacer referencia a SQLNCLI. h y SQLOLEDB. h en el mismo programa, siempre que se defina primero SQLOLEDB. h.|  
|sqlncli11.lib|El archivo de biblioteca necesario para llamar directamente a las funciones de la utilidad **BCP** que forman parte del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client. **Nota:**  Si hace referencia al archivo sqlncli11. lib en el código de programación, debe asegurarse de que el archivo de sqlncli11.dll está en la ruta de acceso del sistema y en la ruta de acceso del sistema de los usuarios que usan la aplicación.|  
  
## <a name="see-also"></a>Consulte también  
 [Generar aplicaciones con SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  
