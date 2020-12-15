---
description: SQLXML no se instala en SQL Server
title: SQLXML no se instala en SQL Server
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e3c588a22c8a55419fac480ed3e38186c37ee148
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97429663"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQLXML no se instala en SQL Server
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Antes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], SQLXML 4.0 se comercializó junto con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y formó parte de la instalación predeterminada de todas las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], salvo [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la última versión de SQLXML (SQLXML 4.0 SP1) ya no está incluida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar SQLXML 4,0 SP1, descárguelo desde la [Ubicación de instalación de sqlxml 4,0 SP1](https://www.microsoft.com/download/details.aspx?id=30403).  
  
 Si una aplicación se ejecuta en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y requiere sqlxml 4,0, tiene que descargar e instalar sqlxml 4,0 SP1.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>Comportamiento de SQLXML 4.0 SP1 con nuevos tipos de datos que usan el proveedor OLE DB de SQLOLEDB y SQL Server Native Client  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] se introdujeron los siguientes tipos de datos, que los desarrolladores que usan SQLXML pueden querer usar:  
  
-   **Fecha**  
  
-   **Time**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 Al usar SQLXML 4,0 SP1 con SQLOLEDB o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , estos tipos aparecen como cadenas para un desarrollador. SQLXML 4,0 SP1 habilitará estos cuatro nuevos tipos de datos como tipos escalares integrados cuando se usan con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de cliente nativo 11,0 o posterior. Hasta que descargue SQLXML 4.0 SP1, la asignación de estos tipos a tipos que no sean de cadena puede producir el truncamiento de algunos datos. Por ejemplo, la asignación de **DateTime2** a **xsd: Date** hará que los datos se trunquen a la [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] precisión de **DateTime** de 3,33 milisegundos.  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos de programación en SQLXML 4.0](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
