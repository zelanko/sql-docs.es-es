---
title: Cuándo usar SQL Server Native Client | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
ms.assetid: 08f18b36-209d-4cf7-9623-ebc61859a91d
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 04f833f288df4a9b85e73ca6401eeb536672e4a8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32950620"
---
# <a name="when-to-use-sql-server-native-client"></a>Cuándo debe utilizarse SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client es una tecnología que puede utilizar para tener acceso a los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Para obtener una explicación de las tecnologías de acceso a datos diferentes, consulte [mapa de carreteras de tecnologías de acceso de datos](http://go.microsoft.com/fwlink/?LinkID=179186)  
  
 A la hora de decidir si debe usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client como la tecnología de acceso a datos de su aplicación, debe tener en cuenta varios factores.  
  
 En el caso aplicaciones nuevas, si está utilizando un lenguaje de programación administrado, como Microsoft Visual C# o Visual Basic, y necesita obtener acceso a las nuevas características introducidas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debería utilizar el proveedor de datos de .NET Framework para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que forma parte de .NET Framework.  
  
 Si está desarrollando una aplicación basada en COM y necesita obtener acceso a las nuevas características introducidas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debería utilizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Si no necesita obtener acceso a las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede seguir utilizando Windows Data Access Components (WDAC).  
  
 En el caso de aplicaciones OLE DB y ODBC existentes, el problema principal es si necesita obtener acceso a las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si su aplicación es antigua y no necesita las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede seguir usando WDAC. Sin embargo, si es necesario tener acceso a esas características nuevas, como el [tipo de datos xml](../../t-sql/xml/xml-transact-sql.md), debe usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Tanto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client como MDAC admiten el aislamiento de transacción de lectura confirmada mediante el uso de versiones de fila, pero solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite el aislamiento de transacción de instantánea. (En términos de programación, el aislamiento de transacción de instantánea con versiones de fila es igual que la transacción de lectura confirmada).  
  
 Para obtener información sobre las diferencias entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y MDAC, consulte [actualizar una aplicación a SQL Server Native Client de MDAC](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
## <a name="see-also"></a>Vea también  
 [Programación de SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Temas de procedimientos de ODBC](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Temas "Cómo..." de OLE DB](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
