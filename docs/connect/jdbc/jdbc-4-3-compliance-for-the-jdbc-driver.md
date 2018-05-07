---
title: JDBC 4.3 compatibilidad para el controlador JDBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be781d51418184aa519854c1ebd6bb59c19ff5b8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC 4.3 compatibilidad para el controlador JDBC
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

    
> [!NOTE]  
>  Las versiones anteriores a 6.4 de controlador JDBC de Microsoft para SQL Server son compatibles con las especificaciones de la API de Java Database Connectivity 4.2. En esta sección no se aplica a las versiones anteriores a la versión 6.4.  
  
 Actualmente, 6.4 de controlador JDBC de Microsoft para SQL Server es Java 9 compatible, pero no es totalmente compatible con las especificaciones de 4.3 de API de conectividad de base de datos de Java. Para recién introducidas las API de JDBC 4.3, si no compatibles con el controlador, el controlador lanzará un SQLFeatureNotSupportedException.