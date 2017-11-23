---
title: "SQLXML no está instalado en SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ee759b9c94f2bbc8a7f0c8cb1595600f29959a87
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQLXML no se instala en SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]Antes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], SQLXML 4.0 se comercializó con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y formó parte de la instalación predeterminada de todos los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versiones excepto [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la última versión de SQLXML (SQLXML 4.0 SP1) ya no está incluida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar SQLXML 4.0 SP1, descárguelo desde [ubicación de instalación para SQLXML 4.0 SP1](https://www.microsoft.com/en-us/download/details.aspx?id=30403).  
  
 Si una aplicación se ejecuta en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y requiere SQLXML 4.0, tiene que descargar e instalar SQLXML 4.0 SP1.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>Comportamiento de SQLXML 4.0 SP1 con nuevos tipos de datos que usan el proveedor OLE DB de SQLOLEDB y SQL Server Native Client  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]incluyen a los siguientes tipos de datos, podrían desear utilizar que los desarrolladores de SQLXML:  
  
-   **Fecha**  
  
-   **Time**  
  
-   **DateTime2**  
  
-   **DateTimeOffset**  
  
 Cuando se utiliza SQLXML 4.0 SP1 con SQLOLEDB o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], estos tipos aparecen como cadenas a un desarrollador. SQLXML 4.0 SP1 habilitará estos cuatro nuevos tipos de datos como tipos escalares integrados cuando se usa con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo proveedor OLE DB Client 11.0 o una versión posterior. Hasta que descargue SQLXML 4.0 SP1, la asignación de estos tipos a tipos que no sean de cadena puede producir el truncamiento de algunos datos. Por ejemplo, la asignación **DateTime2** a **xsd: Date** hará que los datos se trunquen a la [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] **DateTime** precisión de 3,33 milisegundos.  
  
## <a name="see-also"></a>Vea también  
 [Conceptos de programación en SQLXML 4.0](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md)  
  
  
