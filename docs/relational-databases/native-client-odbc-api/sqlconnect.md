---
title: SQLConnect | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLConnect function
ms.assetid: 6da74e3a-4388-4907-81cb-987389bae467
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9ce37c60d4dce64f1e85d31f367b8eb5885926ae
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006626"
---
# <a name="sqlconnect"></a>SQLConnect
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Cuando se abre una conexión, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client establece SQL_COPT_SS_MUTUALLY_AUTHENTICATED y SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD en el método de autenticación que se utiliza para abrir la conexión. Para obtener más información acerca de los SPN, consulte [nombres de entidad de seguridad de servicio &#40;spn&#41; en conexiones de cliente &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="sqlconnect-support-for-high-availability-disaster-recovery"></a>Compatibilidad de SQLConnect para la alta disponibilidad con recuperación de desastres  
 Para obtener más información sobre el uso de **SQLConnect** para conectarse a un [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] clúster, consulte [SQL Server Native Client compatibilidad con la alta disponibilidad y la recuperación ante desastres](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLConnect función)](https://go.microsoft.com/fwlink/?LinkId=101541)   
 [ODBC API Implementation Details](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
