---
title: Preguntas más frecuentes (P+F) sobre ODBC en Linux y macOS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 65bfd6d2-c83d-4528-a5e1-a85b125a4f4a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b266913d6e8e1a073c8831880ddcd4938b2b9dc9
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921927"
---
# <a name="frequently-asked-questions-faq-for-odbc-linux-and-macos"></a>Preguntas más frecuentes (P+F) sobre ODBC en Linux y macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Las siguientes son respuestas a preguntas sobre ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y MacOS.
  
## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

**¿Cómo funcionan las aplicaciones existentes de ODBC en Linux o MacOS con el controlador?**  
Debe poder compilar y ejecutar las aplicaciones de ODBC que ha estado compilando y ejecutando en Linux o MacOS con otros controladores. 
  
**¿Qué características de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] admite esta versión del controlador?**

El controlador ODBC en Linux y MacOS es compatible con todas las características de servidor de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], excepto LocalDB. Para obtener más información sobre las características compatibles de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md).  
  
**¿Es compatible el controlador con la autenticación Kerberos?**  
Sí. Si tiene una configuración del entorno de Kerberos existente, debe poder conectarse a los servidores mediante la opción de cadena de conexión o DSN `Trusted_Connection=Yes`. Para obtener más información, vea [Using Integrated Authentication](../../../connect/odbc/linux-mac/using-integrated-authentication.md) (Uso de la autenticación integrada).  
  
**¿Qué codificación Unicode deben utilizar las aplicaciones?**  
UTF-8 para datos de SQL_CHAR y UTF-16 para datos de SQL_WCHAR. Dependiendo de la configuración regional del sistema y la versión del controlador, es posible que también se admitan los datos que no son UTF-8 de una de varias codificaciones. Para obtener más información, consulte [Instrucciones de programación](../../../connect/odbc/linux-mac/programming-guidelines.md).

**¿Hay ejemplos de ODBC que pueda descargar y ejecutar con el controlador para experimentar con él o evaluarlo?**

Consulte el artículo sobre el [uso de muestras de ODBC con C++ de MSDN existentes para el controlador ODBC en Linux](https://blogs.msdn.com/b/sqlblog/archive/2012/01/26/use-existing-msdn-c-odbc-samples-for-microsoft-linux-odbc-driver.aspx) para obtener una muestra. Esto también es aplicable al controlador ODBC de macOS. 

**¿Es el controlador ODBC en Linux o macOS de código abierto?**

No, los controladores ODBC en Linux y macOS no son un producto de código abierto.  

## <a name="see-also"></a>Consulte también

- [Instalación de Microsoft ODBC Driver for SQL Server en Linux](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Instalación de Microsoft ODBC Driver for SQL Server en macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)
