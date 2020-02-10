---
title: SQLXML no se instala en SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fe1d4b937e5972eb90e567ded91f7a23af577d0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66012159"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQLXML no se instala en SQL Server
  Antes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], SQLXML 4.0 se comercializó junto con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y formó parte de la instalación predeterminada de todas las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], salvo [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la última versión de SQLXML (SQLXML 4.0 SP1) ya no está incluida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para instalar SQLXML 4,0 SP1 cuando esté disponible, descárguelo desde la [Ubicación de instalación de SQLXML SP1](https://www.microsoft.com/download/details.aspx?id=16978).  
  
 Si una aplicación se ejecuta en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y requiere SQLXML 4.0, y si el equipo no tiene instalado [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], deberá descargar e instalar SQLXML 4.0 SP1.  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>Comportamiento de SQLXML 4.0 SP1 con nuevos tipos de datos que usan el proveedor OLE DB de SQLOLEDB y SQL Server Native Client  
 
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] introduce los siguientes tipos de datos, que los desarrolladores de SQLXML pueden usar:  
  
-   `Date`  
  
-   `Time`  
  
-   `DateTime2`  
  
-   `DateTimeOffset`  
  
 Cuando se usa SQLXML 4.0 SP1 con SQLOLEDB (de Data Access Components para Windows, anteriormente Microsoft Data Access Components) o el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], estos nuevos tipos aparecerán como cadenas para el desarrollador. SQLXML 4.0 SP1 habilitará estos cuatro nuevos tipos de datos como tipos escalares integrados cuando se usan con el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client11.0. Hasta que descargue SQLXML 4.0 SP1, la asignación de estos tipos a tipos que no sean de cadena puede producir el truncamiento de algunos datos. Por ejemplo, la `DateTime2` asignación `xsd:date` a hará que los datos se trunquen a la [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] `DateTime` precisión de 3,33 milisegundos.  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos de programación en SQLXML 4.0](sqlxml-4-0-programming-concepts.md)  
  
  
