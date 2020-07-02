---
title: Cuándo usar
description: Decida si va a usar SQL Server Native Client, que es una de las diversas tecnologías que puede usar para tener acceso a los datos de una base de datos de SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
ms.assetid: 08f18b36-209d-4cf7-9623-ebc61859a91d
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9c431eeeefaddc5829d8bf199a2b4b10e1f39bff
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787579"
---
# <a name="when-to-use-sql-server-native-client"></a>Cuándo debe utilizarse SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client es una tecnología que puede utilizar para tener acceso a los datos de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Para obtener una explicación de las distintas tecnologías de acceso a datos, vea [Data Access Technologies Road Map](https://go.microsoft.com/fwlink/?LinkID=179186) (Guía básica de las tecnologías de acceso a datos).  
  
 A la hora de decidir si debe usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client como la tecnología de acceso a datos de su aplicación, debe tener en cuenta varios factores.  
  
 En el caso aplicaciones nuevas, si está utilizando un lenguaje de programación administrado, como Microsoft Visual C# o Visual Basic, y necesita obtener acceso a las nuevas características introducidas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debería utilizar el proveedor de datos de .NET Framework para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que forma parte de .NET Framework.  
  
 Si está desarrollando una aplicación basada en COM y necesita obtener acceso a las nuevas características introducidas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debería utilizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Si no necesita obtener acceso a las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede seguir utilizando Windows Data Access Components (WDAC).  
  
 En el caso de aplicaciones OLE DB y ODBC existentes, el problema principal es si necesita obtener acceso a las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si su aplicación es antigua y no necesita las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede seguir usando WDAC. Pero si necesita tener acceso a estas nuevas características, como el tipo de [datos XML](../../t-sql/xml/xml-transact-sql.md), debe usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Tanto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client como MDAC admiten el aislamiento de transacción de lectura confirmada mediante el uso de versiones de fila, pero solo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite el aislamiento de transacción de instantánea. (En términos de programación, el aislamiento de transacción de instantánea con versiones de fila es igual que la transacción de lectura confirmada).  
  
 Para obtener información acerca de las diferencias entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y MDAC, vea [actualizar una aplicación a SQL Server Native Client desde MDAC](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
## <a name="see-also"></a>Consulte también  
 [Programación de SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Temas de procedimientos de ODBC](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Temas de procedimientos de OLE DB](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
