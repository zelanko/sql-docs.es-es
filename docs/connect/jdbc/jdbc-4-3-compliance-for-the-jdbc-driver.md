---
title: JDBC 4.3 compatibilidad para el controlador JDBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3f678f33ec8f2c844bce14daa150f6c135744ff
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2018
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 4.3 compatibilidad para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  Las versiones anteriores a 6.4 de controlador JDBC de Microsoft para SQL Server son compatibles con las especificaciones de la API de Java Database Connectivity 4.2. En esta sección no se aplica a las versiones anteriores a la versión 6.4.  
  
 Actualmente, 6.4 de controlador JDBC de Microsoft para SQL Server es Java 9 compatible, pero no es totalmente compatible con las especificaciones de 4.3 de API de conectividad de base de datos de Java. Para recién introducidas las API de JDBC 4.3, si no compatibles con el controlador, el controlador lanzará un SQLFeatureNotSupportedException.