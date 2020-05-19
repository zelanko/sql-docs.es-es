---
title: Nombres de orígenes de datos y sistemas operativos de 64 bits | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: c2f86810-2775-4ddd-8df7-e8373785a7fc
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d529786fdb8643338c3a0d004c4a409e8e85a420
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704303"
---
# <a name="data-source-names-and-64-bit-operating-systems"></a>Nombres de origen de datos y sistemas operativos de 64 bits
  Para generar y ejecutar una aplicación como una aplicación de 32 bits en un sistema operativo de 64 bits, debe crear el origen de datos ODBC con el Administrador de ODBC de %windir%\SysWOW64\odbcad32.exe.  
  
## <a name="remarks"></a>Observaciones  
 Un sistema operativo Windows de 64 bits tiene dos archivos odbcad32.exe:  
  
-   %SystemRoot%\system32\odbcad32.exe se usa para crear y mantener nombres de origen de datos para las aplicaciones de 64 bits.  
  
-   %SystemRoot%\SysWOW64\odbcad32.exe se usa crear y mantener nombres de origen de datos para las aplicaciones de 32 bits, incluso las aplicaciones de 32 bits que se ejecutan en sistemas operativos de 64 bits.  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
