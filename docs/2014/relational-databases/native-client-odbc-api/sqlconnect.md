---
title: SQLConnect | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLConnect function
ms.assetid: 6da74e3a-4388-4907-81cb-987389bae467
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d5292d3141d6ae520a333827796ca8fc6005be15
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53355460"
---
# <a name="sqlconnect"></a>SQLConnect
  Cuando se abre una conexión, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client establece SQL_COPT_SS_MUTUALLY_AUTHENTICATED y SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD en el método de autenticación que se utiliza para abrir la conexión. Para obtener más información acerca de los SPN, vea [Service Principal Names &#40;SPN&#41; en conexiones cliente &#40;ODBC&#41;](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="sqlconnect-support-for-high-availability-disaster-recovery"></a>Compatibilidad de SQLConnect para la alta disponibilidad con recuperación de desastres  
 Para obtener más información sobre el uso de **SQLConnect** para conectarse a un [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] del clúster, consulte [Compatibilidad de SQL Server Native Client para la alta disponibilidad con recuperación de desastres](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="see-also"></a>Vea también  
 [Función SQLConnect](https://go.microsoft.com/fwlink/?LinkId=101541)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
