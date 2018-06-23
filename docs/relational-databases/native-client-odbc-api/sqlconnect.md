---
title: SQLConnect | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLConnect function
ms.assetid: 6da74e3a-4388-4907-81cb-987389bae467
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b5440bff64349fb8125245961fddb6a54056fb91
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698656"
---
# <a name="sqlconnect"></a>SQLConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Cuando se abre una conexión, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client establece SQL_COPT_SS_MUTUALLY_AUTHENTICATED y SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD en el método de autenticación que se utiliza para abrir la conexión. Para obtener más información acerca de los SPN, vea [nombres principales de servicio &#40;SPN&#41; en las conexiones de cliente &#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="sqlconnect-support-for-high-availability-disaster-recovery"></a>Compatibilidad de SQLConnect para la alta disponibilidad con recuperación de desastres  
 Para obtener más información sobre el uso de **SQLConnect** para conectarse a un [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] de clúster, consulte [SQL Server Native Client Support for High Availability, Disaster Recovery](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="see-also"></a>Vea también  
 [SQLConnect, función](http://go.microsoft.com/fwlink/?LinkId=101541)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
