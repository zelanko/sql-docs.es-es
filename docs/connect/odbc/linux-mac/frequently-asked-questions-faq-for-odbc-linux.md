---
title: Más preguntas frecuentes (P+F) para Linux de ODBC y macOS | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7abe2f2258a13f10d1f2dcd8eeda40539fe2002d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>Más preguntas frecuentes (P+F) para Linux de ODBC y macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Los siguientes son respuestas a preguntas sobre ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Linux y macOS.
  
## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

**¿Cómo funcionan las aplicaciones existentes de ODBC en Linux o Mac OS con el controlador?**  
Debe poder compilar y ejecutar las aplicaciones ODBC que ha estado compilando y ejecutando en Linux o Mac OS con otros controladores. 
  
**¿Las características de [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] esta versión de la compatibilidad del controlador?**

El controlador ODBC en Linux y macOS admite todas las características de servidor en [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)] excepto LocalDB. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] las características admitidas, vea [directrices de programación](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
**¿El controlador admite la autenticación Kerberos?**  
Sí. Si tiene una configuración de entorno de Kerberos existente, debe ser capaz de conectarse a servidores que utilizan el `Trusted_Connection=Yes` opciones de cadena de conexión o DSN. Para obtener más información, consulte [Using Integrated Authentication](../../../connect/odbc/linux-mac/using-integrated-authentication.md).  
  
**¿Qué codificación Unicode deben utilizar las aplicaciones?**  
UTF-8 para datos de SQL_CHAR y UTF-16 para datos de SQL_WCHAR.  

**¿Hay muestras ODBC que pueda descargar y ejecutar con el controlador para experimentar con o evaluarlo?**

Consulte el artículo sobre el [uso de muestras de ODBC con C++ de MSDN existentes para el controlador ODBC en Linux](http://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) para obtener una muestra. Esto también es aplicable para el controlador ODBC macOS. 

**¿Es el controlador ODBC en Linux o macOS código abierto?**

No, los controladores ODBC en Linux y Mac OS no son un producto de código abierto.  

## <a name="see-also"></a>Vea también
[Instalación de Microsoft ODBC Driver for SQL Server en Linux y Mac OS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
